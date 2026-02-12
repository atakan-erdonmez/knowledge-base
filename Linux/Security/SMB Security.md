# Good Practices
## Group & Nologin

For samba users, it is a good practice to have a seperate group (eg sambagroup), then adding users to that group with nologin shell. Example:
```
groupadd sambagroup
useradd -s /sbin/nologin -g sambagroup ela
smbpasswd -a ela
```
This way, they can not escalate privileges.

> 	/var/lib/samba/private/passdb.tdb
> 	Where smbpasswd hashes are stored

