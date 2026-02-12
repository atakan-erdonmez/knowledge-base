Kickstart is a automation tool for system installation. It can use FTP, HTTP or NFS.

## 🔧 1. Prerequisites

- RHEL/CentOS/AlmaLinux server (e.g., `192.168.1.10`)
    
- A client device that can PXE boot
    
- DHCP server (can be on the same or different machine)
    
- TFTP server
    
- HTTP server (e.g., `httpd` or `nginx`)
    
- Kickstart file (e.g., `ks.cfg`)
    

---

## ⚙️ 2. Install required packages

`sudo dnf install dhcp-server tftp-server syslinux httpd`

---

## 🗂 3. Configure the Kickstart file

Create a minimal Kickstart config (`/var/www/html/ks.cfg`): (better use system-config-kickstart)
```
cat > /var/www/html/ks.cfg <<EOF
#version=RHEL9
install
url --url=http://192.168.1.10/rhel/
lang en_US.UTF-8
keyboard us
timezone UTC
rootpw redhat
bootloader --location=mbr
clearpart --all --initlabel
autopart
reboot
%packages
@core
%end
EOF
```


## 🌐 4. Set up HTTP server to host OS files & Kickstart

```
mkdir -p /var/www/html/rhel
mount /path/to/RHEL.iso /mnt
cp -r /mnt/* /var/www/html/rhel/
```

Make sure `httpd` is started:

`sudo systemctl enable --now httpd`

---

## 📡 5. Configure TFTP and PXE boot

Copy PXE boot files:

```
mkdir -p /var/lib/tftpboot/pxelinux.cfg
cp /usr/share/syslinux/pxelinux.0 /var/lib/tftpboot/
cp /mnt/images/pxeboot/{vmlinuz,initrd.img} /var/lib/tftpboot/
```

Create PXE config (`/var/lib/tftpboot/pxelinux.cfg/default`):

```
cat > /var/lib/tftpboot/pxelinux.cfg/default <<EOF
default linux
label linux
  kernel vmlinuz
  append initrd=initrd.img inst.ks=http://192.168.1.10/ks.cfg
EOF
```

Enable TFTP server in `/etc/xinetd.d/tftp` (if using xinetd) or via `tftp.socket` (systemd):

`sudo systemctl enable --now tftp.socket`
`systemctl restart xinetd`

---

## 📦 6. Configure DHCP server (or modify existing)

Sample `/etc/dhcp/dhcpd.conf`:
```

subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
  option routers 192.168.1.1;
  filename "pxelinux.0";
  next-server 192.168.1.10; # kickstart server IP
}
```

Start DHCP server:

`sudo systemctl enable --now dhcpd`

---

## 🚀 7. PXE Boot the Client

1. Enable PXE/Network boot in the BIOS.
    
2. Client gets IP via DHCP, downloads PXE boot files via TFTP.
    
3. PXE loads kernel/initrd and uses `inst.ks=` to fetch Kickstart file.
    
4. Fully automated OS installation begins.


### Kickstart Config File Creation
1. Download system-config-kickstart from dnf, and use GUI to create file
2. Use RedHat's website
3. Change anaconda-ks.cfg file
4. Read manually