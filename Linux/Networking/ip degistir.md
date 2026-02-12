#### 🔹 Interface & Address Management

```
ip a                                       # Show all addresses 
ip link                                    # Show interfaces (shorter than `ip a`) 
ip addr add 192.168.1.100/24 dev eth0      # Add IP to interface 
ip addr del 192.168.1.100/24 dev eth0      # Remove IP  
ip link set eth0 up/down                   # Enable/disable interface 
ip link show eth0                          # Show specific interface details
```

#### 🔹 Routing


```
ip route show                              # Show routing table ip route add default via 192.168.1.1                    # Add default gateway 
ip route del default                       # Remove default gateway
```

#### 🔹 Neighbors (ARP/NDP)
```
ip neigh                                   # Show ARP table 
ip neigh add 192.168.1.10 lladdr XX:XX:XX:XX:XX:XX dev eth0
```
