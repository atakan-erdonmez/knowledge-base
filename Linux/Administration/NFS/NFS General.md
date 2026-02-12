---
tags:
  - NFS
---

Network file system is used in linux/unix systems to share a file, directory, or disk with multiple clients. You export the local directory and clients mount them. Then, they can use the directory as their local directory.[[Samba]] is used to share with windows


- Exporting an NFS means sharing it to outside
- Default port 2049
- Client have to mount NFS share either manually, automatically or using AutoFS (mount when used, unmount when not used for a while)
- NFS communication works using RPC
# Server Setup

### 1. Download Packages
```shell-session
sudo apt install nfs-kernel-server -y
sudo yum install nfs-utils rpcbind libnfsidmap
```
### 2. Enable Services
`systemctl start rpcbind nfs-server nfs-idmap rpc-statd`
### 3. Create NFS Share
`echo '/home/cry0l1t3/nfs_sharing client_ip(rw,sync,no_root_squash)' >> /etc/exports`

- /etc/exports is the main config file
	->rw: enable clients to write
	-> sync: write changes immediately to the disk
	-> no_root_squash: Giren root ise serverda da root yetkisiyle calisir

- /etc/fstab: Controls mounted NFS directories, auto mount at boot


- /etc/sysconfig/nfs: Controls which ports are required RPC services run on

### 4. Export Shares
Use `exportfs -r` command to re-export everything in /etc/exports

- exportfs command
    - exportfs -r : Reexport all directories after modifying /etc/exports
    - exportfs -v : Displays a list of shared files and export options on a server
    - exportfs -a : exports all directories listed in /etc/exports
    - exports -u : Unexport one or more directories
    - showmount -e [IP]: Show mounted RPCs (client & server)
    - rpcinfo -p


>[!Detailed /etc/exports config]+
> We can configure NFS via the configuration file `/etc/exports`. This file specifies which directories should be shared and the access rights for usersettings such as the transfer speed and the use of encryption. NFS s and systems. It is also possible to configure access rights determine which users and systems can access the shared directories and what actions they can perform. Here are some important access rights that can be configured in NFS:
> 
| **Permissions**  | **Description**                                                                                                                                            |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `rw`             | Gives users and systems read and write permissions to the shared directory.                                                                                |
| `ro`             | Gives users and systems read-only access to the shared directory.                                                                                          |
| `no_root_squash` | Prevents the root user on the client from being restricted to the rights of a normal user.                                                                 |
| `root_squash`    | Restricts the rights of the root user on the client to the rights of a normal user.                                                                        |
| `sync`           | Synchronizes the transfer of data to ensure that changes are only transferred after they have been saved on the file system.                               |
| `async`          | Transfers data asynchronously, which makes the transfer faster, but may cause inconsistencies in the file system if changes have not been fully committed. |





# Client Setup
## Mount NFS Share


```
mount -t nfs 10.129.12.17:/home/john/dev_scripts ~/target_nfs
```

> `df -h` to see which NFS share are mounted
> `mount | grep nfs`

>[!NFS] /etc/fstab config
> IP:/nfs_folder /mnt_location nfs default 0 0

# Theorical

### NFS services

- rpcbind: The rpcbind server converts RPC program numbers into universal addresses (rpc protokol kullanan servisleri dogru porta yonlendiriyor. rpc kullanan servis baslarken rpcbind’a hangi portta calistigini soyler o da yonlendirmeyi yapar)
- nfs-server: It enables clients to access NFS shares
- nfs-lock / rpc-statd: NFS file locking. Implement file lock recovery when an NFS server crashes and reboots.
- nfs-idmap: It translates user and group ids into names, and to translate user and group names into ids

### RPC Services
- **rpc.statd** : implements monitoring protocol (NSM) between NFS client and NFS server
- **rpc.mountd** : The running process that receives the mount request from an NFS client and checks to see if it matches with a currently exported filesystem.
- **rpc.idmapd** : Maps NFSv4 names and local UIDs and GIDs
- **rpc.rquotad** : provides user quota information for remote users.
- **rpc.nfsd** – The process that implements the user level part of the NFS Service. It works with the Linux Kernel to meet the dynamic demands of NFS Clients, such as providing additional server threads for NFS Clients to utilize.

**Services at NFS server:**
- nfsd, rpcbind, rpc.statd, rpc.idmapd, rpc.rquotad, rpc.mountd
-
**Services at NFS client:**
- nfsiod, rpcbind




