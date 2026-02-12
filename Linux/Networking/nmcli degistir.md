# General
The basic syntax is `nmcli [OPTIONS] OBJECT {COMMAND | help}`. The main objects you'll work with are:

- `general`: NetworkManager's status and permissions.
    
- `networking`: Overall networking control.
    
- `radio`: Radio switches (Wi-Fi, WWAN).
    
- `connection` (or `con`): Managing network connections.
    
- `device` (or `dev`): Managing network interfaces.

#### 🔹 Check Network Status



```
nmcli device                              # List all interfaces 
nmcli connection                          # List all saved network profiles nmcli general status                            # System networking state
```

#### 🔹 Connect/Disconnect Interfaces

```
nmcli device connect eth0 
nmcli device disconnect eth0
```

#### 🔹 Configure Static IP
```
nmcli con add type ethernet con-name static-eth0 ifname eth0 ip4 192.168.1.100/24 gw4 192.168.1.1 

nmcli con mod static-eth0 ipv4.dns "8.8.8.8 1.1.1.1" nmcli con up static-eth0
```

#### 🔹 DHCP Configuration


```
nmcli con mod eth0 ipv4.method auto nmcli con up eth0
```

#### 🔹 Wi-Fi (useful for laptops or mobile admin setups)


```
nmcli device wifi list nmcli device wifi connect SSID password YOUR_PASSWORD
```