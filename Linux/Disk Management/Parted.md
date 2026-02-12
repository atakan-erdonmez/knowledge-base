parted /dev/sdb \[unit s|MB|B] print : Print drive partition info

parted /dev/sdb mklabel gpt/msdos : Create partition table

parted /dev/sdb

mklabel gpt : create new GPT table?
mkpart : Create a new partiion
`mkpart primary ext4 0% 100%`

NOTE: In MBR, prompt asks you primary or extended? But in GPT, that is not the case.

With `blkid` command, you can find the UUID of disks. You can also use `lsblk --fs` with `systemctl daemon-reload` you can soft reload all daemons. After changing /etc/fstab, you should use this command.

- Adding disk to virtual machine
    
    To add disk to your virtual machine, these are the steps.
    
    Identify:
    
    `fdisk -l` will show how many disks are connected
    
    `fdisk -l 2> /dev/null | egrep ‘^Disk’ | wc -l` will also show disk number
    
    `fdisk -l 2> /dev/null | egrep ‘^Disk’ | grep -v mapper | grep -v identifier` will show the best resultsfile:
    
    Add disk: In virtual machine settings add disk with your skill.
    
    Mounting: List different connectors (SATA,SCSI,IDE etc.) with commands
    
    `ls /sys/class/fc_host`
    
    `ls /sys/class/scsi_host`
    
    Then, in folder that which `ls` command returned something type these for all hosts
    
    `echo "- - -" > /sys/class/scsi_host/host0/scan`
    
    `echo "- - -" > /sys/class/scsi_host/host1/scan`
    
    etc...
    
    “- - -” are wildcards for **channel**, **SCSI target ID** and **LUN**. The dashes act as wildcards meaning “rescan everything”
    
    After, you can check again if the disk is added with
    
    `fdisk -l 2> /dev/null | egrep ‘^Disk’ | grep -v mapper | grep -v identifier`
    
    