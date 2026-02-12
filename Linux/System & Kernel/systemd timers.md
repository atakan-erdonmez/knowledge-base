## 🧠 What Is a `systemd timer`?

- A **system-level alternative to `cron`**
- Provided by `systemd` (not DNF-specific)
- Uses `.timer` and `.service` unit files
- Can run scripts, services, updates, anything — just like cron
---

## 🔧 How It Works

### A `systemd timer` consists of two files:

1. A `.timer` file — defines **when** to run
2. A `.service` file — defines **what** to run

Example:

- `/etc/systemd/system/mybackup.timer`
    
- `/etc/systemd/system/mybackup.service`


#### Example .service
```
[Unit]
Description=Daily Admin Maintenance Script
# Ensures the script only runs after the network is up, which is useful for
# tasks like updates, backups, or logging to a remote server (like nexonet.space)
After=network-online.target

[Service]
# Set the user to run the script as (e.g., 'root' for full admin tasks)
User=root
# 'oneshot' is used for tasks that run once and then exit
Type=oneshot
# The actual command to execute
ExecStart=/usr/local/bin/admin.sh
# Standard output and error output are routed to the systemd journal
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

#### Example .timer
```
[Unit]
Description=Run admin.service daily at 12:00 PM
# The service this timer controls
Requires=admin.service

[Timer]
# OnCalendar sets the exact schedule: everyday at 12:00 (noon)
OnCalendar=*-*-* 12:00:00
# RandomizedDelaySec staggers the execution time by up to 5 minutes to
# prevent multiple timers on your server from firing at the exact same moment.
RandomizedDelaySec=5min
# Persistent=true is useful for servers: if the system is off at 12 PM, 
# the job will execute shortly after the server boots up.
Persistent=true

[Install]
WantedBy=timers.target
```

Then,

```
sudo systemctl daemon-reload
sudo systemctl enable --now admin.timer
```
## Automatic System Updates

With the use of systemd-timers, you need specific packages for system updates.
- Debian -> unattended-upgrades
- RedHat -> dnf5-automatic

### To edit in Fedora:
```
systemctl list-timers --all | grep dnf
sudo systemctl cat dnf5-automatic.timer
sudo systemctl edit dnf5-automatic.timer

sudo systemctl restart dnf5-automatic.timer

systemctl list-timers dnf5-automatic.timer

```