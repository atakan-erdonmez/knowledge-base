### Install
```
yum install cifs-utils samba-client
```

A program to connect Windows SMB 
[CheatSheat](https://github.com/irgoncalves/smbclient_cheatsheet)

### List shares:
```shell-session
smbclient -L IPaddressOfTarget -U htb-student
```

```
smbclient -L //sambaserver.example.com -N
```

### SMB Password
After useradd, you have to specify a smb password via:
```
smbpasswd -a atakan
```
### Testparm
To check the config if eveyrhing is fine

### Connect to SMB share:

```shell-session
smbclient //<target>/<share$> -U username%password

```

### Mount SMB share

```shell-session
ataker@htb[/htb]$ sudo mount -t cifs -o username=htb-student,password=Academy_WinFun! //ipaddoftarget/"Company Data" /home/user/Desktop/

you can only write username, password will be asked

```

# See Mounted SMB Shares
`findmnt -t cifs`
`smbclient -L localhost`