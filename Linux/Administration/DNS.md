google.com ->
google: SLD (Second Level Domain)
.com: TLD (Top Level Domain)


dig +trace google.com -> see all name server & path: Root -> TLD -> Generic TLD (gTLD)-> SLD

# DNS Server Setup
## 1. Install Packages
```
sudo yum install bind bind-utils
sudo apt install bind9 bind9-utils
```

`systemctl status named`
## 2. Config /etc/named.conf
```
options{
	listen-on port 53 { 127.0.0.1; any;} ;
	allow-query    { localhost; any; } ;
	allow-transfer     ## for slave DNS server, redundancy 
}
```
---

### Zones
```
zone "example.com" IN {
    type master;
    file "fwd.example.com.db";
    allow-update { none; };
};

zone "43.168.192.in-addr.arpa" IN {
    type master;
    file "43.168.192.db";
    allow-update { none; };
};

```
#### 🔍 Explanation (Line by Line)

##### 🔹 First Zone: `example.com`

- `zone "example.com"` → This is the **domain name** being served.
    
- `IN` → Class of the DNS record (always `IN` for Internet).
    
- `type master` → This server is the **authoritative** (primary) source for this zone.
    
- `file "fwd.example.com.db"` → The actual DNS data is stored in this file (`/var/named/fwd.example.com.db` or similar).
    
- `allow-update { none; };` → Disables dynamic updates from clients.
    

🧠 This is a **forward lookup zone** — it maps **names to IPs** (e.g., `www.example.com → 192.168.43.10`).

---

##### 🔸 Second Zone: `43.168.192.in-addr.arpa`

This is the **reverse zone**.

- `zone "43.168.192.in-addr.arpa"` → Special syntax used for **reverse DNS**, i.e., IP → hostname.
    
    - Example: `192.168.43.10` → `host1.example.com`
        
- `file "43.168.192.db"` → Stores reverse mappings.
    
- Same `master` and `allow-update` logic.
    

🧠 Reverse zones are important for:

- Logging
- Mail servers (PTR record checks)
- Diagnostics (e.g., `nslookup 192.168.43.10`)

##### ✅ How Do You Decide What to Write?

##### For a forward zone:

- Define your **domain name** (e.g., `example.com`)
- Create a zone file like `fwd.example.com.db`
- Add **A**, **CNAME**, **MX**, etc. records

##### For a reverse zone:

- Take your **network IP range**, reverse the first 3 octets, and append `.in-addr.arpa`
    - For `192.168.43.x` → `43.168.192.in-addr.arpa`
- Create a reverse zone file (e.g., `43.168.192.db`)
- Add **PTR** records pointing IPs to hostnames
##### 📁 Files You Must Create

These files should exist in `/var/named/` (or wherever your `named.conf` expects):

- `/var/named/fwd.example.com.db`
    
- `/var/named/43.168.192.db`


# 3. Config DNS Data (/etc/named/files.db)

| Options                                                                       | Description                                                                       |
| ----------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| $TTL 3D                                                                       | Takes 3 day for the DNS server to ask for DNS queries to the Authorative server   |
| Name, Class, Type, Data (@, IN, SOA, servera.example.com. root.example.com. ) |                                                                                   |
| Serial (YYYY/MM/DD/HH)                                                        | You need to change this for slave server's to update. It is a timestamp basically |
| Refresh (second)                                                              | Tells to slave server that how often you should check master DNS server           |
| Retry (second)                                                                | Time for slave to try connecting with master if master not responding             |
| Expire                                                                        | If master is not responding for this amount of time, consider master dead         |
| Minimum TTL                                                                   | Keep in the cache for this amount                                                 |


> named-checkconf /etc/named.conf -> Check for syntax 


> `sudo rdnc flush` -> flush local DNS cache


# Alternatives
While **BIND** is foundational and widely used (especially in teaching), it's **old-school**, **complex**, and not the most practical or modern option in many real-world setups today.
## ✅ Practical, More Modern DNS Server Options

### 1. **Unbound** (for DNS **resolvers**)

- Lightweight, secure, caching DNS resolver
    
- Good for **home DNS**, **internal use**, **recursive queries**
    
- Config is much simpler than BIND
    
- Used as the default resolver in many OSes and security appliances (e.g., pfSense)
    

**Use case**: You want to **resolve** domains (e.g., for a local network or ad-blocking)

---

### 2. **dnsmasq** (for **simple DNS + DHCP**)

- Tiny, fast, easy to configure
    
- Can serve DNS + DHCP together
    
- Perfect for local development, home networks, and embedded devices (e.g., routers)
    

**Use case**: Hostnames for your LAN devices, caching resolver, small local zones

---

### 3. **CoreDNS** (modern, plugin-based)

- Used by **Kubernetes** and cloud-native setups
    
- Simple zone and forwarding configuration
    
- Dynamic and extensible with plugins
    
- Great for **internal DNS**, service discovery, container environments
    

**Use case**: You need **internal DNS in cloud/devops** environments (K8s, containers)

---

### 4. **PowerDNS**

- Modern alternative to BIND with API, SQL backend
    
- Scalable and used in ISPs and hosting providers
    
- Split into authoritative and recursive servers
    

**Use case**: Large-scale deployments, custom DNS records from DB/API

---

### 5. **AdGuard Home / Pi-hole**

- Web UI, easy config
    
- Internal DNS, DHCP, ad-blocking
    
- Perfect for home networks and Raspberry Pi
    

**Use case**: You want a **GUI-based**, privacy-respecting, local DNS + ad-blocker

---

## 🔧 Summary Table

|Tool|Purpose|Easy?|Good For|
|---|---|---|---|
|BIND|Authoritative DNS|❌|Legacy, teaching, advanced configs|
|Unbound|Recursive resolver|✅|Home DNS, security setups|
|dnsmasq|DNS + DHCP|✅✅|Routers, dev labs, embedded|
|CoreDNS|Dynamic DNS|✅✅|Kubernetes, service discovery|
|PowerDNS|Authoritative DNS|⚠️|ISP-grade setups, DB integration|
|AdGuard/Pi-hole|GUI local DNS|✅✅✅|Home use, ad-blocking, Raspberry Pi|