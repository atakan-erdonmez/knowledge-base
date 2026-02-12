# **How to write the config file**
/etc/prometheus/prometheus.yml

## Main Sections

### 1. `global`

Applies to all jobs unless overridden:

```yaml
global:   scrape_interval: 15s       # How often Prometheus pulls metrics   evaluation_interval: 15s   # How often rules/alerts are checked   
scrape_timeout: 10s        # How long to wait before a scrape is considered failed external_labels:       
	monitor: 'example'     # Extra label(s) added to every metric
```

**Key setting:** `scrape_interval` — shorter means fresher data but more load.

---

### **2. `alerting`**

Tells Prometheus where your **Alertmanager** is:

```yaml
alerting:
  alertmanagers:
  - static_configs:
    - targets: ['localhost:9093']
```

If you’re not using Alertmanager, you can remove or ignore this section.

---

### **3. `rule_files`**

Lists files that contain **recording rules** or **alerting rules**:

```
rule_files:
  - "first_rules.yml"
```

Rules are YAML files that define conditions and create new metrics or alerts.

---

### **4. `scrape_configs`**

Defines **what targets Prometheus scrapes**:

```
scrape_configs:
  - job_name: 'prometheus'
    scrape_interval: 5s       # Overrides global for this job
    scrape_timeout: 5s
    static_configs:
      - targets: ['localhost:9090']
```

**Important keys:**

- **`job_name`** → Logical label grouping (appears as `job=` in metrics)
    
- **`targets`** → List of `host:port` where metrics live
    
- **`metrics_path`** (default `/metrics`) → Path to scrape
    
- **`scheme`** (default `http`) → Change to `https` if needed
    

You can add more jobs for other exporters, e.g.:

```
  - job_name: 'proxmox-node'
    static_configs:
      - targets: ['192.168.1.10:9100']
```

> The "prometheus" job is only for showing the scrape performance, target health etc, not CPU and RAM. You need to install node_exporter and use port 9100 for that.
---

## **How to define your own config**

1. **Set global settings** for scrape/evaluation intervals.
    
2. **List each target** (exporter) under `scrape_configs` with a `job_name`.
    
3. (Optional) **Override intervals** per job if you want more or less frequent scrapes.
    
4. (Optional) **Add rules** via `rule_files`.
    
5. If using Alertmanager, add it under `alerting`.