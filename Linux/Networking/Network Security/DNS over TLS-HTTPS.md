For DNS over TLS, you need to create a config file in /etc/systemd/resolved.conf.d/ like this:

```
[Resolve]
DNS=1.1.1.1#cloudflare-dns.com 8.8.8.8#dns.google
FallbackDNS=9.9.9.9#dns.quad9.net
DNSOverTLS=yes
Cache=yes
```


## DoT vs DoH

| Feature        | DoT (TLS)            | DoH (HTTPS)                            |
| -------------- | -------------------- | -------------------------------------- |
| Port           | 853                  | 443                                    |
| Protocol       | TLS over TCP         | HTTPS over TLS                         |
| Blocks easier? | Easier (853 blocked) | Harder (hidden in HTTPS)               |
| Purpose        | Pure DNS encryption  | DNS encrypted + mixed into web traffic |

Related:
[[systemd-resolved]]
