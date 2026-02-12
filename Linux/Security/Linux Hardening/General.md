### Disable and remove non-secure programs

Like ftp, telnet, rlogin, rsh services

### Minimize software
Don't install unnecessary packages

### Keep system updated
Pretty self explanatory, right?

### Lockdown cronjobs
`echo ALL >> /etc/cron.deny`

### Turn of IPv6
```
sudo nano /etc/sysctl.d/99-disable-ipv6.conf

net.ipv6.conf.all.disable_ipv6 = 1 net.ipv6.conf.default.disable_ipv6 = 1 net.ipv6.conf.lo.disable_ipv6 = 1

sudo sysctl -p
```
### Disable USB stick to detect
```
sudo nano /etc/modprobe.d/blacklist-usb-storage.conf

# Prevents the usb-storage kernel module from loading, disabling most USB drives. 
install usb-storage /bin/true

# Unloads the driver if it's currently loaded sudo modprobe -r usb-storage
```
**To reverse this,** simply delete the `/etc/modprobe.d/blacklist-usb-storage.conf` file and reboot.

- You can use [[USBGuard]] 

## Password history enforcement
#### On RHEL / Fedora / CentOS (Modern Versions)

These systems use the `pam_pwquality` module to check password policies. The easiest way to configure it is by editing its configuration file.

1. **Edit the `pwquality.conf` file:**
    
```
sudo nano /etc/security/pwquality.conf
```

2. **Add or uncomment the `remember` option:** Find the line for `remember` (it might be commented out with a `#`) and set it to the number of passwords you want to store.

```
# Number of old passwords to remember
remember = 5
```

#### On Debian / Ubuntu

These systems typically configure the `pam_unix` module directly in a central file used by other services.

1. **Edit the `common-password` PAM file:**

```
sudo nano /etc/pam.d/common-password
```

2. **Add `remember=5` to the `pam_unix.so` line:** Find the line that contains `password [success=1 default=ignore] pam_unix.so obscure sha512`. Add the `remember=5` option to the end of it.

**It should look like this when you are done:**

```
password    [success=1 default=ignore]  pam_unix.so obscure sha512 remember=5
```


This securely enables password history without overriding the strong default hashing algorithm (`sha512`).


## Keep /boot Read-Only
In `/etc/fstab`, put `defaults,ro`
## Disable ICMP Ping & Broadcast
### 🔧 Temporarily Disable ICMP (Until Reboot)

`sudo sysctl -w net.ipv4.icmp_echo_ignore_all=1`

To re-enable:
`sudo sysctl -w net.ipv4.icmp_echo_ignore_all=0`

---

### 🛠️ Permanently Disable ICMP (Persists After Reboot)

Edit the `sysctl` config file:
`sudo nano /etc/sysctl.conf`

Add this line at the bottom:
`net.ipv4.icmp_echo_ignore_all = 1`

Then apply the changes:
`sudo sysctl -p`

### Disable Broadcast
Edit `/etc/sysctl.conf`

`net.ipv4.icmp_echo_ignore_broadcast = 1`
(Permanent)

Then apply the changes:
`sudo sysctl -p`

## asdf