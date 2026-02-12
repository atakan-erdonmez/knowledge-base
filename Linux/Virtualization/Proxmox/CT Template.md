- Update system
- Install packages (opnssh-server net-tools curl vim)
- Add default user
- Disable root login and password auth
- Clean machine specific data
```
rm -f /etc/ssh/ssh_host_*
rm -rf /var/log/*
truncate -s 0 /etc/machine-id
ln -sf /etc/machine-id /var/lib/dbus/machine-id
apt clean && apt autoremove -y
history -c
```

[[VM Template & Cloud-init]]

Note: /etc/ssh/ssh_host_* files are for SSH and SSHD service, which are HOST keys, not USER keys.

## After cloning

`ssh-keygen -A` to create HOST SSH keys.