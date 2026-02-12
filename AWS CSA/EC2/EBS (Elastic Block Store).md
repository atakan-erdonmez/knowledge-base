Elastic Block Store is a network drive that you attach. It persists.
They are bound to specific AZ
Low cost, low performance
Good for long-term storage

## Volume Types
There are 6 types of volumes
1. **gp2/gp3 (SSD):** General purpose SSD, price-performance 
2. **io1/io2 Block Express (SSD):** Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads (**provisioned IOPS**). Great for database workloads. They support multi-attach
3. **st1 (HDD):** Low cost HDD volume designed for frequently access, throughput-intensive workloads like big data, data warehouses, log processing etc
4. **sc1 (HDD):** Lowest cost HDD volume designed for less frequently accessed workloads 

> **Only gp2/gp3 and io1/io2 Block Express can be used as boot volumes**

### Multi-Attach
- Only available in io1/io2 Block Express
- Up to 16 EC2 instances at a time
- Must use a file system that's cluster-aware (not XFS, EXT4 etc)

### EBS Encryption
- Has minimal impact on latency
- Leverages keys from KMS (AES-256)

To encrypt an EBS volume, you need to create a snapshot, copy it and encrypt it, then create a volume from it

Or you can take an unencrypted snapshot, create volume from it and while doing that, enable encryption
### Snapshots
Backup of EBS
Not necessary to detach the volume, but *recommended*
- You can copy snapshots across AZ or region
#### Snapshot Features
- EBS Snapshot Archive: Move snapshot to "archive" tier which is %75 cheaper
- Takes within 24-72 hours for restoring the archive
#### Recycle Bin for EBS Snapshots
Retention period to recover accidental deletion
- Setup rules to retention (1 day to 1 year)
#### Fast Snapshot Restore (FSR)
- It is a fast snapshot that takes no latency on initialization, expensive