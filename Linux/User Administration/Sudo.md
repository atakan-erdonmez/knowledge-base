
## Flags

`-S` : Read the sudo password from STDIN

root ALL=(ALL:ALL) ALL → root USER can use ALL COMMANDS in ALL HOSTS in be-like ALL USERS AND GROUPS

( %groupname is group)

$USER host=(user:group) COMMAND

4 types of alias:

1. Host_Alias: 127.0.0.1, 192,168.2.1
2. User_Alias: atakan, consultant
3. Cmnd_Alias: /usr/bin/kill, /usr/bin/mount
4. Runas_Alias: root, operators

Examples:

- User_Alias MANAGERS=james, bill, steve
- Cmnd_Alias READ: /usr/bin/top, /usr/bin/htop
- Host_Alias OP: 127.0.0.1, 192.168.2.100, printer
- MANAGERS OP=(ALL) NOPASSWD:READ

Runas: Sudo komutu girildiginde kim yerine gececegini soyler