---
tags:
  - VPN
  - Networking
---

dnf install wireguard-tools
Uses port 51820/udp

```
sudo wg-quick down wg0 
sudo wg-quick up wg0
wg show
```
# Server Setup

### Generate Keys
	`wg genkey | tee privatekey | wg pubkey > publickey`
### Configure
/etc/wireguard/wg0.conf
```
[Interface]
PrivateKey = <server-private-key>
Address = 10.0.0.1/24
ListenPort = 51820

[Peer]
PublicKey = <client-public-key>
AllowedIPs = 10.0.0.2/32

```

> Enable IP forwarding:

```
echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

### Enable
sudo systemctl enable --now wg-quick@wg0

# Client Setup

`qrencode -t ansiutf8 < /etc/wireguard/wg0.conf`



## Related:
[[qrencode]]
