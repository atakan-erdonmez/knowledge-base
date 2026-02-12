
## Server Installation

```
apt install -y prometheus
```


This installs:

- Service: prometheus.service
- Config: /etc/prometheus/prometheus.yml
- Data dir: /var/lib/prometheus
- Listens on :9090

Enable and start:

```
systemctl enable --now prometheus
systemctl status prometheus --no-pager
```

> Note: Prometheus keeps the data and saturates the storage. You can see it with `sudo du -sh /var/lib/prometheus`.

Default retention period is 15 days.
## Node-Scraper Installation

https://prometheus.io/docs/guides/node-exporter/#tarball-installation

mv node_exporter* /usr/local/bin/
useradd --no-create-home --shell /usr/sbin/nologin nodeusr
nano /etc/systemd/system/node_exporter.service

```
[Unit]
Description=Prometheus Node Exporter
After=network.target

[Service]
User=nodeusr
ExecStart=/usr/local/bin/node_exporter
Restart=always

[Install]
WantedBy=default.target
```

## Check config
`promtool check config /etc/prometheus/prometheus.yml`