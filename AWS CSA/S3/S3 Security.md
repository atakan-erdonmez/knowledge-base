# MFA Delete
It is additional security when you want to do destructive actions, like permanently delete an object version, or SuspendVersioning on the bucket.
- Only the root account can enable/disable MFA delete

> You have to connect with CLI to enable it. You can't enable/disable from the console as of now.


# Access Logs
You can log all access to S3 buckets. Any request made to S3 will be logged into **another** S3 bucket, from any account, authorized, or denied
- The target bucket **must be different from the source bucket** and should be in the same region

To enable it, you have to create a bucket for logging. Then, in the bucket you want to log, you should enable 'server access logging'.


# Pre-Signed URLs
They are temporary access to specific locations. They are signed by your signature, so they inherit your set permissions. They expire after set duration.
- Can be created by S3 Console, CLI, or SDK

You can go to object -> object actions -> share with presigned url

# S3 Glacier Vault Lock
It locks your Glacier vault, so you or anyone can **never** delete an object. Vault lock policy can never be changed.

- Adopts WORM model (Write Once Read Many)
- Helpful for compliance and data

## S3 Object Lock
> Versioning must be enabled

It blocks an object version deletion for a specified amount of time. There are 2 modes:
**Compliance**: Versions cannot be overwritten or deleted by anyone. Retentions can't be changed, period can't be shortened
**Governance**: Most users can't overwrite or delete. Some users have special permissions for these.

> Legal hold: Protect the object indefinitely, independent from retention period. You can delete it manually


# S3 Access Points
It is an entry point to prefixes in your bucket. You can create different access points for finance and sales for example. It simplify security management.
- It has its own DNS name (Internet Origin or VPC Origin)

### VPC Origin
You can define access points VPC-only. You must create VPC Endpoint to access the Access Point

### Object Lambda
Lambda functions can be used to change the object before it is retrieved by the caller application.

- If you want to redact some information from the original data, you don't have to keep 2 separate buckets, for normal and redacted versions.
- Instead, you can have Lambda function set up with Lambda Access Point to redact data on the fly.
- You can redact PII, convert data formats, resize, watermark images etc