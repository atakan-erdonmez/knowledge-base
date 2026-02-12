### 1 · Install the build tools



```
apt update
apt install -y git build-essential autoconf automake libtool \                pkg-config libusb-1.0-0-dev libudev-dev libssl-dev
```

_Why?_ gcc/make and Autotools compile the code; libusb / libudev headers let the driver talk to USB.

---

### 2 · Grab the latest NUT source and prepare it


```
cd /usr/src 
git clone https://github.com/networkupstools/nut 
cd nut 
./autogen.sh               # creates the ./configure script
```

_Why?_ Debian’s packaged NUT is older; we need master because it contains the _armac_ sub‑driver.

---

### 3 · Configure the build for your UPS and the **nut** account

```
./configure --prefix=/usr --sysconfdir=/etc/nut \
	--with-usb --with-drivers=nutdrv_qx \
	--with-user=nut --with-group=nut \             
	--without-doc
```

_Why?_ `nutdrv_qx` (+ _armac_) is the only driver we need; `--with-user/group` tells the daemons which account to run under.

---

### 4 · Compile and install

```
make -j"$(nproc)" 
make install 
systemctl daemon-reload
```

_Why?_ Copies binaries and the vendor udev rule **`62‑nut‑usbups.rules`** into `/lib/udev/rules.d`.

---

### 5 · Describe the UPS to NUT

Create **`/etc/nut/ups.conf`**

```
[tuncmatik]   
driver     = nutdrv_qx   
port       = auto   
vendorid   = 0925   
productid  = 1234   
subdriver  = armac   
protocol   = Q1
```

_Why?_ The driver reads this block to know how to open the device.

---

### 6 · Minimal server and shutdown configuration

- `/etc/nut/nut.conf`

```
MODE=standalone
```


- `/etc/nut/upsd.conf`

```
LISTEN 127.0.0.1
```


- `/etc/nut/upsd.users`


```
[upsmon]
	password = changeme   
	upsmon   master
```

- `/etc/nut/upsmon.conf`

```
MONITOR tuncmatik@localhost 1 upsmon changeme master FINALDELAY 30
```

_Why?_ These four files let `upsd` serve data locally and `upsmon` shut the host down on low battery.

---

### 7 · Make sure the **nut** user can open the USB node

1. Create the user if it doesn’t exist:
    
    `adduser --system --group --no-create-home nut`
    
2. Re‑enumerate the UPS so the vendor rule takes effect:
    
    `udevadm control --reload-rules udevadm trigger -v -s usb -a idVendor=0925 -a idProduct=1234   # or just re‑plug`
    
3. Confirm:
    
    `ls -l /dev/bus/usb/*/* | grep 0925    # should be root:nut  crw-rw----`
    

_(If it isn’t, drop your own rule in `/etc/udev/rules.d/90-local-ups.rules` with `GROUP="nut", MODE="0660"`.)_

---

### 8 · Enable and start the daemons


```
systemctl enable nut-driver.target nut-server.service nut-monitor.service systemctl restart nut-driver.target sleep 2
```

---

### 9 · Verify

```
upsc tuncmatik@localhost | head
```

You should see lines such as  
`input.voltage: 229.7` `battery.voltage: 13.5` `ups.status: OL`

---

### 10 · If you still get **“Driver not connected”**

1. Check driver log:
    
    `journalctl -u nut-driver@tuncmatik -n 20 --no-pager`
    
    _Most common cause:_ USB node not writable by **nut** → fix udev rule.
    
2. After fixing, re‑trigger udev and restart driver:
    
    `udevadm trigger -v -s usb -a idVendor=0925 -a idProduct=1234 systemctl restart nut-driver@tuncmatik`
    

Once `upsc` works, Proxmox will shut down cleanly when the UPS battery reaches `LB`.