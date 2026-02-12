![[AWS storage types.png]]

It is a bridge between on-premises data and cloud data

**Use cases**:
- disaster recovery
- backup & restore
- tiered storage 
- on-premises cache & low-latency files access

**Types of Storage Gateway:**
- S3 File Gateway
- Volume Gateway
- Tape Gateway

# S3 File Gateway
> Used for *non-glacier* S3 buckets

Configured S3 buckets are accessible using NFS and SMB protocol. You connect to S3 File Gateway, and it connects to the backend S3 bucket via HTTPS. 
- Most recently used data is cached in the file gateway
- Doesn't support Glacier, but you can use Lifecycle Policy
- Gateway uses IAM to access S3
- SMB has integration with AD
![[S3 file gateway.png]]
# Volume Gateway
Block storage using iSCSI backed by S3. 
- Backed by EBS snapshots which can help restore on-premises volumes
- **Cached volumes:** low latency access to most recent data, data stored in S3 and cache is on-prem
- **Stored volumes:** entire dataset is on premise, scheduled backups to S3 with EBS Snapshots
![[AWS Volume Gateway.png]]

# Tape Gateway
Used for physical tape backup. Same process, but in cloud
- Virtual Tape Library (VTL) backed to S3 and Glacier, back up using existing tape-based process and iSCSI interface