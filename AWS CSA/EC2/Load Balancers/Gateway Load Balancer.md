Deploy, scale, and manage a fleet of 3rd party network virtual appliances in AWS, like IDS/IPS, firewall, DPI etc

- Operates at Layer 3 - IP Packets
- Combines the following functions:
	- **Transparent Network Gateway** - single entry/exit for all traffic
	- **Load Balancer** - distributes traffic to your virtual appliances

- Uses **GENEVE** protocol on port **6801**


### Target Groups
- EC2 instances
- IP Addresses

![[AWS - Gateway Load Balacner.png]]