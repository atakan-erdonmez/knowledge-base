Package: vsftpd
Daemon: vsftpd
Ports: 20,21
Config file: ==/etc/vsftpd/vsftpd.conf==

When vsftp installed, ftp user is created with home dir /var/ftp

/var/ftp -> anonymous user jail
/var/ftp/pub -> user public folder

> [!note]
> FTP is not suitable for multi-user fine-grained security purposes. It has 2 main purposes: *public sharing without write perm*, and *download/upload capability for users on the server*

| Config File Options =\[YES/NO] | Uses                                                                                                                                               |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| anonymous_enable               | Enable anonymous user login                                                                                                                        |
| local_enable                   | Any user with a password on the local systems can login                                                                                            |
| write_enable                   | Allow write commands: STOR, DELE,RNFR, RNTO, MKD, RMD, APPE, and SITE                                                                              |
| local_umask \[022]             | The value of umask for file creation, set for local users                                                                                          |
| anon_upload_enable             | Enable upload from anon users                                                                                                                      |
| anon_mkdir_write_enable        | Enable creation of new directories by anonymous users                                                                                              |
| listen                         | Run vsftpd in standalone mode (?)                                                                                                                  |
| userlist_enable                | Enable using userlist to blacklist or whitelist. Need to be enabled for the coming 2 options                                                       |
| userlist_deny                  | If set to YES, every user in the *userlist_file* will be **DENIED**. If set to NO, **only users in the file can log in**, everyone else is denied. |
| userlist_file                  | Specify userlist file                                                                                                                              |
| chroot_local_user              | Local users will be placed in chroot() jail in their home director. **Definitely use**                                                             |
| local_max_rate                 | Maximum data transfer rate permitted for local clients                                                                                             |
| anon_max_rate                  | Maximum data transfer rate permitted for anonymous users                                                                                           |
| no_anon_password               | No password for anonymous                                                                                                                          |
| allow_writeable_chroot         | Allow writing permission when chroot is enabled (try not to use)                                                                                   |
## FTP Client
- ftp \[client]
- ftp> open IP
- ftp> disconnect
- get -> download
- put -> upload
You can't re-login without disconnecting

With using **!command**, you can run the command on your local machine instead of FTP server 

# FTP Problems
1. chroot_local_user can cause security problems. To use this, **the folder should NOT be writable**

> [!chroot problem]+
> allow_writable_chroot
> allow_writeable_chroot
> 
> First one doesn't work, only second does. First one is used in extended vsftpd build (vsftpd-ext)
> [Resource](https://www.benscobie.com/fixing-500-oops-vsftpd-refusing-to-run-with-writable-root-inside-chroot/)
> 


# FTP Security

>[!Best Security Practices for FTP]
>- Disable anonymous login
>- Use userlist
>- Enable local user & chroot_local_user
>- Only chmod 777 /var/ftp/pub, not /var/ftp


