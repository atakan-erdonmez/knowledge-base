## 🧱 Core Concepts First

### 📄 **Logs**: Messages your system/services write (e.g., login, ssh attempt, sudo usage, nginx error).

These logs need to be:

1. **Collected** → from files or services
    
2. **Processed** → filtered, formatted
    
3. **Stored** → saved in a searchable format
    
4. **Viewed/Alerted** → through a UI or alert system
    

---

## 🧰 CATEGORY: **Log Collection and Shipping**

| Tool          | What It Does                                                                                      | Role                             |
| ------------- | ------------------------------------------------------------------------------------------------- | -------------------------------- |
| `syslog`      | Generic term for standard UNIX-style logging (not a tool)                                         | Logging format                   |
| `journald`    | Part of systemd. Collects system logs and stores in binary                                        | Default logger on modern systems |
| `rsyslog`     | A powerful log router. Takes logs from journald/files and sends them elsewhere                    | Log shipper                      |
| **Filebeat**  | Lightweight agent from Elastic. Reads log files and sends to another service (e.g., ELK, Graylog) | Log shipper                      |
| **Logrotate** | Not a logger — it rotates old logs to avoid disk bloat                                            | Log maintenance                  |
| **Promtail**  | Lightweight agent from Grafana Labs. Scrapes logs from local files and sends them to Loki.        | Log shipper                      |

---

## 🛡️ CATEGORY: **Security Auditing & Intrusion Detection**

| Tool           | What It Does                                                                | Role                     |
| -------------- | --------------------------------------------------------------------------- | ------------------------ |
| **Falco**      | Real-time detection of suspicious behavior using syscalls (via eBPF)        | Runtime threat detection |
| **auditd**     | Kernel-level logging of access to files, syscalls, etc. Very detailed       | Security audit trail     |
| **Lynis**      | One-time or scheduled audit of system security (permissions, configs, etc.) | Security scanner         |
| **RKHunter**   | Scans for known rootkits, trojans                                           | Malware scanner          |
| **Chkrootkit** | Similar to RKHunter                                                         | Malware scanner          |

---

## 📊 CATEGORY: **Log Viewing & SIEM Dashboards**

| Tool        | What It Does                                                          | Role                  |
| ----------- | --------------------------------------------------------------------- | --------------------- |
| **Grafana** | Beautiful dashboards and charts (data visualization tool)             | UI                    |
| **Loki**    | Grafana’s log storage/search engine (like Elasticsearch but for logs) | Stores & queries logs |
| **Graylog** | All-in-one centralized log manager with UI, alerts, parsing, etc.     | Full SIEM             |
| **Wazuh**   | Full-featured SIEM with agents and dashboards                         | SIEM/IDS              |
| **Kibana**  | UI for Elasticsearch (used in ELK stack)                              | UI for logs/metrics   |

---

## 📬 CATEGORY: **Alerting / Reporting**

|Tool|What It Does|Role|
|---|---|---|
|**Logwatch**|Sends daily summary of logs (cron-friendly)|Simple email report|
|**Falco**|Sends alerts on suspicious actions|Real-time alerts|
|**Grafana**|Can send alerts based on log queries or metrics|Alert platform|

---

## 🔄 Example: How They Work Together

### 💡Scenario: You want to monitor your server for attacks and logs

**Option A – Classic Stack:**

```
System (journald/syslog) → rsyslog → Graylog → [You view in web UI]      
			↘→ auditd/Falco → alerts                   
			↘→ Logwatch → daily summary
```

**Option B – Grafana Stack:**

```
journald/syslog → promtail/filebeat → Loki                           
						↘→ Falco → alerts                           
						↘→ Grafana → UI for logs + dashboards
```

---

## 🧭 TL;DR Cheat Sheet

|Tool|Log Collector?|Log Viewer?|Security Alerts?|UI?|
|---|---|---|---|---|
|journald|✅|❌ (CLI only)|❌|❌|
|rsyslog|✅|❌|❌|❌|
|auditd|✅|❌|✅ (raw)|❌|
|Falco|✅|✅ (raw logs)|✅|❌|
|Grafana+Loki|✅|✅|✅|✅|
|Graylog|✅|✅|✅|✅|
|Wazuh|✅|✅|✅|✅|