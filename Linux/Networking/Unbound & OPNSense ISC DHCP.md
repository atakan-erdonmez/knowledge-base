In order to give static IPs to devices with hostnames, you have 2 options

## Option 1

If used static IPs in devices itself, you can override them to put custom hosts.

To do that, go here in OPNSense

**Services → Unbound DNS → Overrides → Host Overrides**

> You also have Alias option, which is used for having multiple domain names to a single IP. You can define a host override to add a domain to IP, and create Alias override to have multiple domains.

## Option 2

Reserve specific IP addresses to MAC addresses, so even devices that want to use static IP can enable DHCP.

**Services → DHCPv4 → \[Your Interface]**

In **DHCP Static Mappings**, add the host.