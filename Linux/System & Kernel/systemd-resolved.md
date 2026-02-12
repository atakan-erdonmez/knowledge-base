# Systemd-resolved
✅ `systemd-resolved` is a **built-in DNS resolver/manager daemon in systemd-based distros.**

→ Handles:

- DNS resolution
    
- DNS caching
    
- DNSSEC
    
- DNS-over-TLS
    
- Split DNS per network
    
- Updates `/etc/resolv.conf` dynamically
    

It listens on `127.0.0.53` → intercepts DNS queries from apps.

Acts like a local DNS forwarder → sends to configured upstream DNS servers.

>/etc/systemd/resolved.conf -> config file
## resolvectl

👉 `resolvectl` is a **command-line tool** to interact with `systemd-resolved` (the DNS manager daemon).

It’s like a **control/status utility** for systemd-resolved.

You can use it to:

- Check current DNS servers
    
- See which DNS servers are used per network interface
    
- See if DNS-over-TLS is enabled
    
- Test DNS queries manually
    
- Flush DNS cache
    
- Change DNS config dynamically
### 📝 **Example commands:**

* Check status:

> `resolvectl status`

* Query a DNS name:

> `resolvectl query google.com`

* Flush DNS cache:

> `resolvectl flush-caches`




## /etc/resolv.conf & /etc/systemd/resolved.conf

/etc/resolv.conf is a symlink to systemd/resolved.conf. It is used by third party programs for basic purposes.

If not, you can link with 
`ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf`

# Domain
To add your PC to a domain, you can put this entry under /etc/systemd/resolved.conf.d/custom.conf
```
Domains=lan
```
##### What `~lan` means

You've uncovered a subtle but critical detail of `systemd-resolved`'s configuration. The tilde `~` prefix has a very specific meaning: it tells the resolver to **only** use this domain as a "DNS search scope". It's a technical setting that essentially says, "I am authoritative for this domain, so if a query comes in for `somehost.lan`, I can answer it, but don't automatically append `.lan` to unqualified names."

Essentially, it's the `~` that's preventing your system from automatically adding `.lan` to your `nslookup proxmox1` query.