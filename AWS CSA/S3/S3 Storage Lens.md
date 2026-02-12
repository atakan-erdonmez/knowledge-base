It is a service to understand, analyze and optimize storage across whole AWS organization. It is a reporting program basically
- Discover anomalies, identify cost efficiencies, apply data protection best practices
- Aggregate data for Organization, specific accounts, regions, buckets, or prefixes
- Default dashboard or custom dashboard
- Can be configured to export metrics daily to an S3 bucket (CSV, Parquet)

# Metrics

### Summary Metrics
- General insights about your S3 storage
- StorageBytes, ObjectCount...
- Use cases: identify the fastest-growing (or not used) buckets and prefixes

### Cost-Optimization Metrics
- Provide insights to manage and optimize storage costs
- NonCurrentVersionStorageBytes, IncompleteMultipartUploadStorageBytes
- Use cases: identify buckets with incomplete multipart uploaded older than 7 days

### Data-Protection Metrics
- Provide insights for data protection features
- VersioningEnabledBucketCount, MFADeleteEnabledBucketCount, SSEKMSEnabledBucketCount...
- Use case: identify buckets that aren't following data-protection best practices

### Access-Management Metrics
- Provides insights for S3 Object Ownership
- ObjectOwnershipBucketOwnerEnforcedBucketCount
- Use cases: identify which Object Ownership settings your bucket use

### Event Metrics
- Provide insights for S3 Event Notifications
- EventNotificationEnabledBucketCount (identify which buckets has S3 Event Notifications configured)

### Performance Metrics
- Insights for S3 Transfer Acceleration
- TransferAccelerationEnabledBucketCount (which buckets have Transfer Acceleration enabled)

### Activity Metrics
- Insights about how storage is requested
- AllRequests, GetRequests, PutRequests...

### Detailed Status Code Metrics
- Insights for HTTP status codes
- 200OKStatusCount, 403ForbiddenErrorCount