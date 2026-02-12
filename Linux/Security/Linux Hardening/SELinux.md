::setroubleshoot ???::
::semanage port::
# Theory

- It is an acronym for Security-enhanced Linux. It is a security feature of the Linux kernel

- SELinux gives you the ability to limit privileges of processes and reduce the damage froma possible system or application vulnerability exploitation. It is based on MAC (Mandatory Access Control)

- SELinux provides an additional layer security over user/group/other perms that is object-based and controlled by more sophisticated rules, known as mandatory access control.

- SELinux is a set of security rules that determine which process can access which files, directories, and ports. Every file, process, directory, and port has a special security label called a SELinux context.


# SELinux Context
SELinux labels have several contexts: **user**, **role**, **type**, and **sensivitiy**. The targeted policy, which is the default policy enabled in RHEL,  bases its rule on the third context: **type context**. Type context names usually end with \_t.

![[SELinux Context.png]]


To see SELinux context of a file:
```
ls -Z
```

To see SELinux context of a process:
```
ps -efZ | grep -i httpd
```

![[SELinux Perms.png]]

# SELinux Modes
1. **Enforced**: Actions contrary to the policy are blocked and a corresponding even is logged
2. **Permissive**: Actions contrary to the policy are only logged in the audit lot.
3. **Disabled**: The SELinux is disabled entirely.

### To switch SELinux mode temporarily:
0 -> Permissive
1 -> Enforcing

`setenforce [ Enforcing | Permissive | 1 | 0 ]`
 OR
 `echo [0|1] > /sys/fs/selinux/enforce`


> If you change to/from to disabled, you have to reboot the system

### To switch SELinux mode permanently:

Edit `/etc/sysconfig/selinux` and set SELINUX parameter
### To see SELinux mode:
`getenforce`

## SELinux status
`sestatus`


# Change Context
## Temporary
`chcon` : Change context

```
chcon -R -t httpd_sys_content_t
recursive, type to this
```

## Permanently
`semanage`

```
semanage fcontexclea
restorecon -v /web
```

To delete permanent context:
`semanage fcontext -d -t httpd_sys_content_t /webdata`

> Subfolder and files inherit 
> If copied from another location, context will change accordingly. But when you move, it won't change.
# Restore Context
```
restorecon -v -R /folder
```
# Booleans
- View all available booleans:
	`getsebool -a`
- View a single boolean's status
	`getsebool ftp_home_dir`
- Get detailed information like current status, default status and description
	`semanage boolean -l`
- Change boolean temporarily
	`setsebool ftp_home_dir [on | off | 1 | 0 ]`
- Change boolean permanently
	`setsebool -P ftp_home_dir on`
- SELinux boolean settings directory:
	`/sys/fs/selinux/booleans`