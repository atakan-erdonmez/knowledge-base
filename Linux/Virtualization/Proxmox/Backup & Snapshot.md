- Backup is in a completely different storage then the VM. It is a full clone of the disk

- Snapshot is a part of the VM. You can't move it elsewhere, and it is inside the VM disk
	- It makes sense when testing a specific software or a config


> [!Include RAM]
> Normally a snapshot is an image of the disk. You can capture the RAM with this, which is more powerful




## Backup Modes
- Snapshot: Least downtime. Live backup. qemu-agent helps consistency
- Suspend: Not suggested via Proxmox. Similar to PC suspend mode
- Stop: Stops the VM, takes the backup (most secure)

## Automatization
In "Datacenter" view and "Backups", you can schedule backup jobs