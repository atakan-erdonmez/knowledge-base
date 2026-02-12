Works on **SMB** (Server Message Block), **CIFS** (Common Internet File System), and **NMB** (NetBIOS Message Block).

- SMB is used in **file sharing** and NMB in **domain sharing**.

# Config
#### Packages
samba*.rpm
`smbd --version`
#### Ports
- 137 NetBIOS name service (NetBIOS network browsing)
- 138 NetBIOS datagram service (NetBIOS name service)
- 139 NetBIOS session service (file & printer sharing)
- 445 (NetBIOS & CFIS)
#### Configuration file
- /etc/samba/smb.conf
#### Service Daemon 
- smb -> 139/445 TCP
- nmb -> 137/138 UDP
`systemctl start smb`
`systemctl start nmb`

> SMB is for actual sharing of files and printers
> NMB is for naming of the devices via NetBIOS and browsing the network in Windows Explorer
#### Mounting
- Linux: `mount //sambaserver/dvd -o username=john`
- Windows: `map \\sambaserver\pen`
##### Same OS
![[SMB File Share Same OS.png]]

##### Different OS
![[Samba between different OS.png]]





## Administration
### SMB Password
After useradd, you have to specify a smb password via:
```
smbpasswd -a atakan
```
### Testparm
To check the config if eveyrhing is fine

![[smbclient#See Mounted SMB Shares]]
