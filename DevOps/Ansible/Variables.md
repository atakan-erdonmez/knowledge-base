Stores information that varies with each host

In playbook.yaml:
```
name:
hosts:
vars:
	dns_server: 10.1.250.10
```

In separate file
```
variable1: value1
```

## Variable Precedence
To assign a variable to a group, you can do:

```yaml
...

[web_servers]
web1
web2
web3

[web_servers:vars]
dns_server=10.5.5.3
```

>[!note]
>Precedence hierarchy:
>Extra vars (while running playbook) > Play vars > Host vars > Group vars



## Variable Scope
| Scope  | Where it lives            | When to use it                                        |
| ------ | ------------------------- | ----------------------------------------------------- |
| Global | ansible.cfg or Env vars   | For system-wide settings like SSH users.              |
| Group  | group_vars/webservers.yml | When you want all your servers to share a setting.    |
| Host   | host_vars/pi-brain.yml    | For settings unique to one specific server            |
| Task   | Inside a specific task    | For a one-time setting, like a temporary folder path. |

#### Example File
```
# --- Host Definitions ---
[web_servers]
# Host variable wins over everything else
raspbi ansible_host=192.168.1.50 storage_path=/mnt/ssd_usb

[db_servers]
db_pi ansible_host=192.168.1.51

# --- Group Variables ---
[web_servers:vars]
http_port=80
is_exposed=true

# --- Parent Group Definitions ---
[lab:children]
web_servers
db_servers

# --- Global/Parent Variables ---
[lab:vars]
ansible_user=atakan
ansible_ssh_private_key_file=~/.ssh/id_rsa
```


## Magic Variables
### hostvars
You can access other hosts' variables using 'hostvars' magic variable

`msg: '{{ hostvars['web2'].ansible_host }}'`

### groups
It shows you all the hosts that belong to the specific group
`msg: '{{ groups['america_servers'] }}'`

### group_names
It shows you all the group the host is part of
`msg: '{{ group_names }}'`
