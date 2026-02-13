A list of instances to manage. You can use IP or hostname. You can group them as well

```yaml
server1.company.com
server2.company.com

[mail]
192.168.10.10
server3.company.com
```


## Alias
You can specify an alias by using ansible_host parameter

```ini
web ansible_host=server1.company.com
db ansible_hsot=server2.company.com
```
ansible_host is used to specify an FQDN or an IP

There are other inventory parameters, like:
- ansible_connection: ssh/winrm/localhost
- ansible_port: 22/5986
- ansible_user: root/administrator
- ansible_ssh_pass: Password
```
web1 ansible_host=server1.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!
```

## Parent Groups, ini vs yaml format

For a small company, basic ini format is fine. But for complex orgs, you would need yaml

#### ini formating

```ini
[web_servers]
web1 ansible_host=server1.company.com
server2.company

[db_servers]
sql1.company
sql2.company

[all_servers:children]
web_servers
db_servers
```


#### yaml formatting
```yaml
all:
	children:
		webservers:
			hosts:
				web1.example.com
				web2.example.com
		dbservers:
			hosts:
				db1.example.com
				db2.example.com
```