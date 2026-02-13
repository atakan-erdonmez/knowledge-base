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

```
web ansible_host=server1.company.com
db ansible_hsot=server2.company.com
```
ansible_host is used to specify an FQDN or an IP

There are other inventory parameters, like:
- ansible_connection: ssh/winrm/localhost
- ansible_port: 22/5986
- ansible_user: root/administrator
- ansible_ssh_pass: Password