Launch 3rd party high-performance file systems on AWS. Fully managed service
- FSx for Lustre
- FSx for Windows File Server
- FSx for NetApp ONTAP
- FSx for OpenZFS

## FSx for Windows File Server
Fully managed Windows file system shared drive.
- Supports SMB & Windows NTFS
- Active Directory integration, ACLs, user quotas
- **Can be mounted on Linux EC2 instances**
- You can use Microsoft Distributed File System (DFS) Namespaces to group multiple file systems together, like connecting on-premise and cloud

## FSx for Lustre
Lustre is a type of parallel distributed file system, for large-scale computing. The name is derived from "Linux" and "cluster".

- Used for machine learning, **High Performance Computing (HPC)**, video processing, financial modeling, electronic design automation
- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies
- Seamless integration with S3, read and write with S3
- Can be used from on-premises servers (VPN or Direct Connect)


## FSx for NetApp ONTAP
Managed NetApp ONTAP on AWS. (ONTAP is a proprietary OS from NetApp for network systems)
- File system compatible with NFS, SMB, iSCSI
- Move workloads running on ONTAP or NAS, works with linux, windows, macos, vmware cloud...
- Storage shrinks and grows automatically
- Snapshots, replication, lost-cost, compression and data de-duplication
- Point-in-time instantaneous cloning (helpful for testing new workloads)

## Amazon FSx for OpenZFS
- File system compatible with NFS (v3, v4, v4.1, v4.2)
- Move workloads running on ZFS, works with linux, macos, windows, amazon workspaces, appstream...
- Up to 1.000.000 IOPS with < 0.5ms latency
- Snapshots, compression and low cost; Point-in-time instantaneous cloning


## FSx File System Deployment Options
2 file system:

### Scratch File System
- Temporary storage, data not replicated
- High burst (6x faster, 200MBps per TiB)
- Usage: short-term processing, optimize costs

### Persistent File System
- Long-term storage, data replicated within same AZ
- Replace failed within minutes
- Usage: long-term processing, sensitive data