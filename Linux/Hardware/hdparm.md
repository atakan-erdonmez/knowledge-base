It is a program used for managing hard disk parameters, like spinning it down
https://wiki.archlinux.org/title/hdparm



### ✅ `hdparm` Parameters (for your notes)

|Command|Description|
|---|---|
|`-B 254`|Sets **APM** (Advanced Power Management) to **disable head parking** (max performance)|
|`-S 60`|Sets **spindown timeout** to **5 minutes** (60 × 5 sec = 300 sec)|
|`-I /dev/sdX`|Shows detailed disk info (including current APM level, spindown)|
|`-y`|Forces **immediate spindown** (for testing)|
|`-C`|Checks current power state (active/standby)|

---

### 🛠️ `/etc/hdparm.conf` Example

ini

CopyEdit


```
/dev/sdb {
	apm = 254     
	spindown_time = 60 
}
```

- `apm = 254` → disables head parking
    
- `spindown_time = 60` → spin down after 5 min idle
    

You can repeat the block for multiple drives (`/dev/sda`, `/dev/sdc`, etc).


### Recommendation: A Better Way to Spin Down USB Drives

Instead of the low-level `hdparm`, you should use the modern `udisksctl` utility, which works at a higher level and is designed to handle various connection types, including USB.

To spin down (power off the spindle of) your drive, use [[udisksctl]]:



```
udisksctl power-off -b /dev/sdd
```