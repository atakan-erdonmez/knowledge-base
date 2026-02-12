You have two options to use templates in proxmox: Cloud-image or manual

It is a program used in deployment. It helps changing stuff that should be unique to the device, like ssh keys
# Manual

## Creation
```
sudo rm -f /etc/ssh/ssh_host_*
sudo truncate -s 0 /etc/machine-id
sudo ln -sf /etc/machine-id /var/lib/dbus/machine-id

sudo apt install qemu-guest-agent -y  
sudo apt clean && sudo apt autoremove -y        # Debian/Ubuntu
sudo dnf clean all && sudo dnf autoremove -y    # RHEL-based
sudo poweroff
```
- Delete ssh_host keys in /etc/ssh
- `sudo truncate -s 0 /etc/machine-id` OR i think you can echo "" to it.
- /var/lib/dbus/machine-id is a link to /etc/machine-id. Make sure it is soft link

**Suggestion**: I would suggest creating the template with main controller PC's public key on it. So you won't need to copy it again and again.


## First boot

```
sudo dpkg-reconfigure openssh-server       # Regenerates SSH host keys
sudo systemctl restart ssh
sudo hostnamectl set-hostname new-name
sudo reboot
```

- When you clone, it will copy the disk info as well. It will re-create the same sized disk.


# Cloud-init
## VM Creation
- In OS, select "Do not use any media"
- In disks, remove all disks
- After creation, remove CD/DVD drives
- Add cloudinit drive (as default, you can put to local)
- We will use a cloud image instead of a disk
#### Cloud image
A cloud image is a pre-made virtual machine disk that is ready to use and designed to be automatically set up using cloud-init when it starts.

Suggested to download via CLI to the location `/var/lib/vz/template/vm_disks`.

### Installation Steps
1- `qemu-img resize cloudimg.qcow2 20G` : This resizes the disk for appropriate use. This is not the actual disk size, just the virtual size. It means the disk can grow up to 20G.

2- `qm importdisk <vm_id> cloudimg.qcow2 local-lvm` : This import the disk to the template you will create. You can specify the location changing the local-lvm. This is the location I use for my VM disks and storage

3- `qm set <vm_id> --serial0 socket --vga serial0` : This enables terminal **RESEARCH**. learn linux tv was saying i couldn't work without it, or maybe another channel

4- In GUI, go to template and Hardware. It will show Unused Disk. Edit and add it

5- Disable network boot via Options > Boot order

6- Convert into a template

Then you can edit cloud-init options.
You might also wanna change /etc/hostname

## Cloud-init Settings

Cloud-init is a tool that automatically sets up a new virtual machine with configurations like hostname, username and networking

Basically adjust accordingly. Suggested to set IP setting to DHCP


#### Linked vs Full clone

# IMPORTANT
Cloud init only exist in VMs. It is used for  ssh key generation, for each vm to have seperate ssh keys.

In containers, you have to run the command:
`sudo dpkg-reconfigure openssh-server`

It re-creates the ssh keys