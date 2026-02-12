sudo sgdisk --zap-all /dev/sdb
sudo sgdisk --backup=/tmp/sda.gpt /dev/sda
```
sudo partprobe /dev/sdb
```

```
sudo sgdisk -e /dev/sdb
```

sgdisk -G


gdisk?? (gpt version of fdisk)


smartctl

sudo smartctl -a /dev/sdX -> check disk health??