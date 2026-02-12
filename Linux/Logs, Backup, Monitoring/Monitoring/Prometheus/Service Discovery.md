Yep — you can mix **static targets** with **service discovery (SD)** so you don’t have to hand-edit IPs every time. Here are the 2 SD methods that work great in a Proxmox homelab, plus how to combine them.

# TL;DR

- Keep a couple of **static** must-scrape targets.
    
- Add **file_sd** (simple local YAML/JSON list you can update without touching main config).
    
- Optionally add **dns_sd** (Prometheus discovers hosts from your DNS; great if you use OPNsense/Unbound).
    

---

# Option A — `file_sd_configs` (recommended for homelab)

Maintain a separate file listing targets. Easy to script and reload.

### `prometheus.yml`



scrape_configs:
  # Static fallback (always scrape these)
  - job_name: 'nodes-static'
    static_configs:
      - targets: ['192.168.10.5:9100']
        labels:
          role: 'hypervisor'

  # Dynamic list from files (add/remove hosts here)
  - job_name: 'nodes-file-sd'
    file_sd_configs:
      - files:
          - /etc/prometheus/targets/nodes.yml
        refresh_interval: 30s

### `/etc/prometheus/targets/nodes.yml`


```
- targets:
  - '192.168.10.20:9100'  # Ubuntu server
  - '192.168.10.21:9100'  # Debian server
  labels:
    role: 'server'
- targets:
  - '192.168.10.30:9100'  # NAS
  labels:
    role: 'storage'
```

> Edit `nodes.yml` to add/remove machines. Prometheus will pick changes automatically (every 30s) — no full restart needed.

---

# Option B — `dns_sd_configs` (uses your DNS)

Let Prometheus resolve a record (A/AAAA or SRV) and scrape all returned endpoints.

### A/AAAA record (simplest)

Create a DNS record (e.g., `nodes.lan`) that returns multiple IPs.

yaml

CopyEdit

`scrape_configs:   - job_name: 'nodes-dns-a'     dns_sd_configs:       - names: ['nodes.lan']   # returns multiple A/AAAA records         type: 'A'         port: 9100         refresh_interval: 30s`

### SRV record (more flexible; per-target ports)

Create SRV like `_node-exporter._tcp.lan` pointing to each node and its port.

yaml

CopyEdit

`scrape_configs:   - job_name: 'nodes-dns-srv'     dns_sd_configs:       - names: ['_node-exporter._tcp.lan']         type: 'SRV'         refresh_interval: 30s`

> In OPNsense → Unbound, you can add A/AAAA or SRV records so adding a new node is just a DNS change.

---

# Mix them together (static + file_sd + dns_sd)

Use all three; Prometheus will dedupe by the target address.

yaml

CopyEdit

`scrape_configs:   - job_name: 'nodes'     scrape_interval: 15s      # 1) Static “must have” targets     static_configs:       - targets: ['192.168.10.5:9100']  # Proxmox      # 2) File-based list maintained by you/scripts     file_sd_configs:       - files: ['/etc/prometheus/targets/nodes.yml']         refresh_interval: 30s      # 3) DNS-based discovery (A/AAAA or SRV)     dns_sd_configs:       - names: ['nodes.lan']         type: 'A'         port: 9100         refresh_interval: 30s`

---

# (Optional) Useful relabeling

Tag instances with a friendly name or drop stray targets.

yaml

CopyEdit

  `- job_name: 'nodes'     file_sd_configs:       - files: ['/etc/prometheus/targets/nodes.yml']      relabel_configs:       # If you put a custom label in file_sd (e.g., role), it’s already attached.       # Here’s an example to copy the target address to a clean "instance" label:       - source_labels: [__address__]         target_label: instance         regex: '([^:]+):.*'         replacement: '$1'        # Example: drop anything that isn't on port 9100       - source_labels: [__address__]         regex: '.+:9100'         action: keep`

---

# Reloading config safely

- Best: enable HTTP reload and POST to it:
    
    - Add `--web.enable-lifecycle` to Prometheus start flags.
        
    - `curl -X POST http://<prometheus-ip>:9090/-/reload`
        
- If you didn’t enable that: `systemctl restart prometheus`