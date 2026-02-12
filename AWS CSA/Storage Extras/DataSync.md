Move large amount of data to and from. 
- On-premises / other cloud to AWS (NFS, SMB, HDFS, S3 API...) - needs agent
- AWS to AWS (different storage services) - no agent needed

Can synchronize to:
- Amazon S3 (any storage classes, including Glacier)
- EFS
- FSx

- Replication tasks can be scheduled hourly, daily, weekly
- File permissions and metadata are preserved


>[!INFO]
> If you don't have enough bandwidth, you can use AWS Snowcone, DataSync agent is preinstalled

