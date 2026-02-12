# Global

- Workgroup should be set to the same as Windows computers.
- hosts allow - 192.168.0.0/24
	- This is suggested. Whitelists hosts

### Public Share
In global, put this:
> `map to guest = bad user`
	(bu cok da ise yaramiyor gibi, her turlu calisiyor, onemli olan guest ok parametresi)

This means, when there is a bad user (wrong password or no username), act as if they are guest.

In the share part, you gotta add
- `guest ok = yes`

# What will be shared?

In the bottom of file, you gotta create a \[] to define what to share. Example:
```
[documents]
	comment = Important documents
	path = /var/importantdocs # Path of shared folder
	browseable = yes/no # If yes, it will be browseable. If no, user must know the name and manually enter
	guest ok = yes/no # If no, user should enter user-password to access (makes it private)
	writeable = yes # Makes it writable
	valid users = @unixadmin # only users in this group will have access to this directory
	
```


