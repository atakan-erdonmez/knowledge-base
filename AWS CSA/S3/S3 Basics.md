It is an object storage.
- They should have globally unique name
- They are defined in region level


# Generic
Objects (files) have a Key
The key is the Full path:
- s3://mybucket_my_file.txt

So the key is prefix + object name.

> There is no concept of 'directories' within buckets, but UI makes it look like it
> Everything is just keys


## Objects
Object values are the content of the body. Max size is 5TB. If uploading more than 5MB, must use 'multi-part upload'.

- Metadata (list of text key/value pairs - system or user metadata)
- Tags (Unicode key/value pair - up to 10) - useful for security / lifecyclc
- Version ID (if versioning enabled)

# Security
The Object URL will be inaccessible by public by default. But when you click 'open', you can view it. This is because it is 'pre-signed' access key, which verifies you are the owner of the data.

#### User-based
- **IAM Policies**: API calls should be allowed for a specific user from IAM
#### Resource-based
- **Bucket Policies**: Bucket-wide rules from the S3 console, allows cross account
- **Object ACL**: Finer grain (can be disabled)
- **Bucket ACL**: Less common (can be disabled)


### Bucket Policies
They are JSON based. It has Sid, effect, principal (user or account), action, and resource.

## Versioning
It is in bucket level, same key overwrite will change the version.
When you delete a file, it will create a delete marker. To completely remove that file, you should remove it again. You can restore it by deleting the 'delete marker'.

# Replication (CRR & SRR)
**CRR**: Cross-Region Replication - compliance, lower latency, replication across accounts
**SRR**: Same-Region Replication - log aggregation, live replication
- Must enable Versioning in source and destination buckets
- Buckets can be in different AWS accounts
- Copying is ASYNC 
> After you enable Replication, only new objects are replicated. To replicate existing, use *S3 Batch Replication*.

- Only delete markers are replicated, not actual 'deletes'