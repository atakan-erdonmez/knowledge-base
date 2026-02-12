There are 2 parts to the alerts:
1- The actual alerts that you define by creating rules
2- AlertManager that takes these alerts and doing actions with them like sending notifications and silencing.

# Rules
You generally keep the rules in `/etc/prometheus/rules`. There can be multiple, and they should be ending with .yml. You should point to these rules in `/etc/prometheus/prometheus.yml`.

- **Example config**:
```
/etc/prometheus/
	prometheus.yml
	rules/
		node.rules.yml
		disks.rules.yml
```


## Rule Syntax
You start with groups, which defines and groups the alerts. 
- Then there is the name, which is the name of the group. You define rules below it.
- You can define alerting and recording rules

> **To check rules: `promtool check rules /etc/prometheus/rules/node.rules.yml`

## Enable Rule
1. Reference the rules in `prometheus.yml`

```yaml
rule_files:
	- /etc/prometheus/rules/*.yml
```

2. Reload prometheus by `sudo systemctl reload prometheus`

### Test Rule
This rule always create an alert, so it can be used to test the alerts.

```yaml
groups:
  - name: test
    rules:
      - alert: AlwaysFiring_Test
        expr: vector(1)
        for: 10s
        labels:
          severity: info
        annotations:
          summary: "Test alert from Prometheus"
```

### Example rule
```yaml
groups:
  - name: node-health
    rules:
      - alert: InstanceDown
        expr: up == 0
        for: 2m
        labels:
          severity: critical
        annotations:
          summary: "Target down: {{ $labels.instance }}"
          description: "Prometheus has not scraped {{ $labels.instance }} for 2 minutes."

      - alert: HighCPUUsage
        expr: avg by(instance) (rate(node_cpu_seconds_total{mode!="idle"}[5m])) > 0.85
        for: 10m
        labels:
          severity: warning
        annotations:
          summary: "High CPU on {{ $labels.instance }}"
          description: "Non-idle CPU usage > 85% for 10m."

      - alert: LowMemory
        expr: (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes) < 0.10
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Low memory on {{ $labels.instance }}"
          description: "Available memory < 10% for 5m."

      - alert: DiskSpace10Percent
        expr: (node_filesystem_avail_bytes{fstype!~"tmpfs|overlay|squashfs"} 
              / node_filesystem_size_bytes{fstype!~"tmpfs|overlay|squashfs"}) < 0.10
        for: 10m
        labels:
          severity: warning
        annotations:
          summary: "Disk almost full on {{ $labels.instance }} ({{ $labels.mountpoint }})"
          description: "Free space < 10% for 10m on {{ $labels.device }} mounted at {{ $labels.mountpoint }}."

```

# AlertManager

This is a program that gets the alerts from Prometheus and take actions upon them. 

- Install & enable:
	`sudo apt install prometheus-alertmanager`
	`sudo systemctl enable --now  prometheus-alertmanager`
	
## 🔹 Key concepts

Routes basically define *which receiver gets which alert.*

- **Root route**
    - Always required.
    - Defines default behavior (grouping, intervals, fallback receiver).
        
- **Sub-routes**
    - Checked in order.
    - Can filter alerts with `matchers` (e.g., `severity="critical"`).
        
- **Receivers**
    - Actual destinations (email, Telegram, Discord, Slack, etc.).
    
- **Grouping**
    - Alerts with the same `group_by` labels are sent together in one message (to avoid spam).
        
- **Intervals**
    - `group_wait`: wait this long before first notification (allows grouping).
    - `group_interval`: minimum time between updates for the same group.
    - `repeat_interval`: re-send if alert is still firing after this long.


## Configuration
### 1. Create the config

Create `/etc/alertmanager/alertmanager.yml` (create the directory, too)

#### Example Alert Config

```yaml
route:
  receiver: default                # default receiver if nothing else matches
  group_by: ['alertname','instance'] # alerts with same labels get grouped
  group_wait: 30s                  # wait before sending first notification
  group_interval: 5m               # minimum wait between notifications for a group
  repeat_interval: 3h              # resend if alert still firing after this time

receivers:
  - name: default                  # must match the route.receiver above
    telegram_configs:              # example: send to Telegram
      - bot_token: "123456:ABC-XYZ"
        chat_id: 123456789
        message: "Alert: {{ .CommonAnnotations.summary }}"
```

`sudo systemctl restart prometheus-alertmanager`

## 2. Point Prometheus to AlertManager

In `/etc/prometheus/prometheus.yml`, add:
```
alerting:
	alertmanagers:
		- static_configs:
			- targets: ['ip:9093']
```

`sudo systemctl reload prometheus`