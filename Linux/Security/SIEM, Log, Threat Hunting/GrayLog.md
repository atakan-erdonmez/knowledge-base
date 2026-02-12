
All-in-one centralized log manager with UI, alerts, parsing, etc.

FULL SIEM


# Installation
Here is a **clean, minimal, step-by-step guide** to install **Graylog Open Source** on your server (Fedora/RHEL/CentOS). Graylog uses **OpenSearch** as backend, and requires **MongoDB** for metadata.

---

## ⚙️ Graylog Stack Overview

|Component|Purpose|
|---|---|
|**Graylog Server**|Core app (UI, rules, API)|
|**OpenSearch**|Stores logs (used to be Elasticsearch)|
|**MongoDB**|Stores Graylog config (dashboards, users)|
|**rsyslog/Filebeat**|Sends logs to Graylog|

---

## ✅ 1. Set Hostname and Timezone (Optional but recommended)

bash

CopyEdit

`sudo hostnamectl set-hostname graylog.local sudo timedatectl set-timezone Europe/Istanbul`

---

## ✅ 2. Install Dependencies

bash

CopyEdit

`sudo dnf install -y epel-release sudo dnf install -y pwgen curl gnupg`

---

## ✅ 3. Install MongoDB (v6+ recommended)

bash

CopyEdit

`cat <<EOF | sudo tee /etc/yum.repos.d/mongodb-org-6.0.repo [mongodb-org-6.0] name=MongoDB Repository baseurl=https://repo.mongodb.org/yum/redhat/\$releasever/mongodb-org/6.0/x86_64/ gpgcheck=1 enabled=1 gpgkey=https://pgp.mongodb.com/server-6.0.asc EOF  sudo dnf install -y mongodb-org sudo systemctl enable --now mongod`

---

## ✅ 4. Install OpenSearch (Graylog-compatible fork of Elasticsearch)

bash

CopyEdit

`sudo rpm --import https://artifacts.opensearch.org/publickeys/opensearch.pgp  cat <<EOF | sudo tee /etc/yum.repos.d/opensearch.repo [opensearch] name=OpenSearch repository baseurl=https://artifacts.opensearch.org/releases/bundle/opensearch/2.x/yum/ gpgcheck=1 gpgkey=https://artifacts.opensearch.org/publickeys/opensearch.pgp enabled=1 autorefresh=1 type=rpm-md EOF  sudo dnf install -y opensearch`

### ⚙️ Minimal Config:

Edit `/etc/opensearch/opensearch.yml`:

yaml

CopyEdit

`cluster.name: graylog node.name: node-1 network.host: 127.0.0.1 http.port: 9200 discovery.type: single-node`

Start OpenSearch:

bash

CopyEdit

`sudo systemctl daemon-reexec sudo systemctl enable --now opensearch`

---

## ✅ 5. Install Graylog Server

bash

CopyEdit

`sudo rpm -i https://packages.graylog2.org/repo/packages/graylog-5.2-repository_latest.rpm sudo dnf install -y graylog-server`

### 🔑 Generate secrets:

bash

CopyEdit

`SECRET=$(pwgen -N 1 -s 96) SHA_PASS=$(echo -n "yourpassword" | sha256sum | cut -d" " -f1)`

---

### ✏️ Edit `/etc/graylog/server/server.conf`

properties

CopyEdit

`password_secret = <SECRET> root_password_sha2 = <SHA_PASS> root_username = admin http_bind_address = 0.0.0.0:9000 elasticsearch_hosts = http://127.0.0.1:9200 mongodb_uri = mongodb://127.0.0.1:27017/graylog`

Replace `<SECRET>` and `<SHA_PASS>` with generated values.

---

## ✅ 6. Start Graylog

bash

CopyEdit

`sudo systemctl daemon-reexec sudo systemctl enable --now graylog-server`

---

## ✅ 7. Access the Web UI

Open:

cpp

CopyEdit

`http://<your-server-ip>:9000`

- **Username**: `admin`
    
- **Password**: what you hashed above (`yourpassword`)
    

---

## 🎯 8. Send Logs to Graylog

Use `rsyslog` or `filebeat` on the same machine or other servers to send logs to Graylog. I’ll guide that after you confirm Graylog is running.

---

Let me know once you're in the dashboard. I’ll help you:

- Create inputs (e.g., Syslog UDP)
    
- Send logs from your system
    
- Create alerts and dashboards
    

Also let me know if you're on **Ubuntu/Debian** — some commands will differ.