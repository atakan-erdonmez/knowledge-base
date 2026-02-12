In this writeup, I am going to talk about how did I configured my HPE Proliant ML150 Gen9 server as router for Turkcell TV+

# Step 0: Understanding & Logic
## VLAN

ISPs deliver multiple services, such as Internet, IPTV and VoIP. Even though they use the same hardware (fiber, VDSL, ADSL), they have to separate them using VLANs, which is a network standard to segregate the traffic (IEEE 802.1Q).

In order to configure a custom device that enables using IPTV, the device should understand these VLAN tags. The WAN side should be configured to listen for VLAN 103 for TV+.

## IGMP & Multicast

Normally, regular internet uses one-to-one (unicast) connection, like when you are connecting to a website.

IPTV however uses multicast, where the ISP sends the stream to multiple nodes, where you "tune in" in order to watch something. Think of it like service, they send it to every IPTV node, and if you want to change the channel to one of the streams, you join the cast.

This process is managed by IGMP (Internet Group Management Protocol). By default, a security-focused firewall like OPNSense blocks all incoming multicast traffic. In order to use it, we have to configure IGMP Proxy.

### What is IGMP Proxy?

Basically IGMP proxy is just a middleman for transferring the traffic between the IPTV device and the multicast from ISP. It listens for IGMP join requests from clients like IPTV device and forward them to the ISP's network. 

It listens on the **downstream** interface, and forward to **upstream** interface.

OPNSense uses os-igmp-proxy plugin to use IGMP proxy. To install, navigate *System > Firmware > Plugins* and install.

## Definitions

**vtnet0**: The WAN port in the OPNSense, it connects to Proxmox bridge 0. It is for incoming connection.
**vtnet1**: The LAN port in OPNSense, it connects to Proxmox bridge 1.

So you need 2 bridges in Proxmox, which should be added in "Hardware" section of the VM

# Step 1: Create VLAN

TV+ uses VLAN 103 for IPTV. So the first step is creating the VLAN.

1. On the OPNSense GUI, navigate *Interfaces -> Devices -> VLAN*
2. Click +
3. Adjust the settings as below:
	- Device: Any name you want, I will use vlan0.103
	- Parent: You should select your WAN device. In my case, I am selecting vtnet0
	- VLAN Tag: 103
	- VLAN Priority: Video (4)
	- Description: Anything you want. I used "TV+ VLAN"
4. Apply and save

This way, we created a low-level "pipe", which we will use for an interface.

> **Note:** This topic is a little hard to grasp. Basically, we created a kernel-level device. Now, we will create a friendly interface that will use this device, which is our VLAN
# Step 2: Assign the VLAN

Now, we will create the interface that we will use from now on. It will use our low-level VLAN.

## Step 2.1: Create Interface

1. Go to *Interface -> Assignments*
2. In the "New Interface" section, you should see your VLAN. Click the "+" button and save it as a new interface.

Now you should be able to see your new interface on the "Interface" menu on the left

## Step 2.2: Configure the Interface

1. Check the "Enable Interface" box.
2. Put the settings as below:
	- Description: Anything you wish, I will use IPTV_WAN
	- IPv4 Configuration Type: Select DHCP
	- IPv6 Configuration type: Select DHCPv6
	- VLAN Priority: Video (4)

So, what we did? We created an interface. Since it uses the VLAN 103, it will get an IP address from the ISP to use IPTV.

Now, go to *Interface > Overview*. You should see IPTV_WAN using the device vlan0.103, and getting an IP address & gateway.

> IF NOT:
> Go to the [[Turkcell TV+ IPTV Setup with OPNSense#Interface Lock|Interface Lock]] section to fix the possible problem.


# Step 3: Configure the IGMP Proxy

1. Go to *Services -> IGMP Proxy*
2. Click *Add* and set like below:
	- **Interface**: Select IPTV_WAN (your new IPTV interface)
	- **Type**: Upstream
	- **Networks**: This is the most critical part. If you are using Superonline TV+, these IP addresses might work. But they might have been changed, so you might have to research. Also, if you use another IPTV provider, these IP addresses will be different. It is your responsibility to have a through research for the IP addresses. You can use AI with deep research mode. These are the settings I used:
		- 172.31.128.0/19
	    - 176.43.0.0/24
	    - 176.235.0.0/20
	    - 10.31.0.0/16
	- **Description**: Anything you want. I put "IPTV Upstream"
3. Click *Save* and add another instance
4. Set as below:
	- Interface: Select LAN
	- Type: Downstream
	- Networks: Leave blank
	- Description: IPTV Downstream
5. Click *Save*, and click the *Enable IGMP Proxy* button on top right.


Until now, if you don't have any firewall or NAT problem, it should be working. The upcoming steps are for security purposes and highly suggested. Also, if you have configured the firewall, or the outbound NAT didn't work as expected, can solve your problem

# Possible Problems
## Interface Lock

In my case, when I checked the *Interface > Overview*, I saw that IPTV_WAN was not active. And when I checked *Interfaces > Assignments*, saw that the vlan0.103 was down, hence the red plug. 

When researching, I encountered a topic called "Interface Lock". I was using this OPNSense as my main router, so the usual ISP router does not exist, so I configured my WAN port as PPPoE.

When I do that, it locked the physical vtnet0 device, so the VLAN couldn't use the vtnet0. Also, I saw that my "WAN" interface is using the pppoe0 (vtnet0) device instead of vtnet0. So the vtnet0 was not used by anything.

In order to solve this, i needed to create another device in the Assignments tab. The only available device was vtnet0, so I created a interface called "vtnet0_lockremover". 

After creating it, I went to VLAN tab again, went to settings and applied without changing anything. I also went to Assignments tab, deleted the IPTV_WAN, and re-created it. This solved my problem

>I got locked out of the device hence the network for some time, but it got solved by itself in 5 minutes.

