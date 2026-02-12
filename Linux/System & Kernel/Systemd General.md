htb-student@nixfund:~$ systemctl cat syslog
 /lib/systemd/system/rsyslog.service

[Unit]
Description=System Logging Service
Requires=syslog.socket
Documentation=man:rsyslogd(8)
Documentation=http://www.rsyslog.com/doc/

[Service]
Type=notify
ExecStart=/usr/sbin/rsyslogd -n
StandardOutput=null
Restart=on-failure

[Install]
WantedBy=multi-user.target
Alias=syslog.service

Via using cat command, we can see the details of the daemon.



`~/.config/systemd/user/` -> for user-level .service files

> [!For user level systemd files]+
> **Reload systemd and enable service**
> systemctl --user daemon-reexec
> systemctl --user daemon-reload
> systemctl --user enable syncthing.service
> systemctl --user start syncthing.service
