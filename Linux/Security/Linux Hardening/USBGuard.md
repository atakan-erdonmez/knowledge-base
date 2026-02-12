**USB Security**

For a much more granular and powerful approach, especially on a server or a security research machine like your ProLiant, **USBGuard** is the professional tool. It allows you to create policies to authorize (whitelist) specific devices while blocking all others by default. You can create rules based on device type, vendor ID, product ID, and even serial number.

This is the best method if you want to allow _only_ your specific keyboard and mouse but block everything else.

### 1. Install USBGuard

On Debian/Ubuntu

```
sudo apt update
sudo apt install usbguard
```

 **On RHEL/Fedora:**

```
sudo dnf install usbguard
```


### 2. Generate an Initial Policy: It's easiest to start by generating a policy that allows all currently connected devices.

```
sudo usbguard generate-policy >   /etc/usbguard/rules.conf
```
**Review this file!** It will contain rules to allow the devices that were plugged in when you ran the command.


### 3. Start and Enable the Service:

```
sudo systemctl enable --now usbguard.service
```


Now, any new USB device you plug in that is **not** in the `rules.conf` file will be blocked.

**To authorize a new device:**

- Plug in the new device. It will be blocked.
    
- Run `usbguard list-devices` to see a list of devices, including the blocked one.
    
- Find the ID of the blocked device and run `sudo usbguard allow-device <id>`.
    
- To make this change permanent, you need to append the device's rule to `/etc/usbguard/rules.conf`. You can do this by running `usbguard generate-policy -a >> /etc/usbguard/rules.conf` while the temporarily allowed device is plugged in.