4 methods to encrypt objects

## Server-Side Encryption (SSE)
#### SSE with Amazon S3-Managed Keys (SSE-S3)
- Enabled by default, encrypt with keys handled, managed and owned by AWS
#### SSE with KMS Key Stored in AWS KWS (SSE-KMS)
- Leverage AWS Key Management Service to manage encryption keys
#### SSE with Customer-Provided Keys (SSE-C)
- Manage your own keys

## Client-Side Encryption


# SSE-S3
- Keys are managed by AWS. Encryption type is AES-256. 
- Header: "x-amz-server-side-encryption":"AES256"
- Enabled by default for new buckets & objects

# SSE-KMS
- Manager your own keys using AWS KMS (Key Management System)
-  KMS advantages: user control + audit key usage using CloudTrail
- Header: "x-amz-server-side-encryption":"aws:kms"
- You have a default key already
## Limitations
- If you use KMS, you may be impacted by KMS limits
- When you upload, it calls the **GenerateDataKey** KMS API, when you download, it calls the **Decrypt** KMS API. This counts towards the KMS quote per second
- You can increase quota using Service Quotas Console

# SSE-C
- AWS does **not** store the encryption key you provide. It is fully managed by customer
- HTTPS must be used, and keys should be provided in HTTP headers in every request

# Client-Side Encryption
- Uses client libraries such as Amazon S3 Client-Side Encryption Library
- Client must encrypt and decrypt data before sending and retrieving to Amazon S3

> DSSE-KMS is a new encryption method that is just "double encryption based on KMS"