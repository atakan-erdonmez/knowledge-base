- S3 Standard - General Purpose
- S3 Standard - Infrequent Access (IA)
- S3 One Zone - Infrequent Access
- S3 Glacier Instant Retrieval
- S3 Glacier Flexible Retrieval
- S3 Glacier Deep Archive
- S3 Intelligent Tiering

S3 is quite durable, and all storage classes have same durability

## S3 Standard Storage Classes

### S3 Standard - General Purpose
- 99.99% Availability
- Used for frequently accessed data
- Low latency and high throughput
- Sustain 2 concurrent facility failures

Use cases: Big data analytics, mobile & gaming applications, content distribution...

### S3 Standard - Infrequent Access
- 99.9% availability
- For less frequently accessed data, but requires rapid access when needed
- Lower cost than S3 standard
Use cases: Disaster recovery, backups

### S3 One Zone - Infrequent Access
- High durability in a single AZ, data lost when AZ is destroyed
- 99.5% availability
Use cases: Storing secondary backup copies of on-premise data, or creatable  

## S3 Glacier Storage Classes
- Low-cost object storage meant for archiving / backup
- Price for storage + object retrieval cost

#### Instant Retrieval
- Milliseconds retrieval, great for data accessed once a quarter
- Minimum storage duration of 90 days
#### Flexible Retrieval 
- Expedited (1 to 5 min), Standard (3-5 hours), Bulk (5-12 hours, free)
- Minimum storage duration for 90 days
#### Deep Archive
- Standard (12 hours), Bulk (48 hours)
- Minimum storage duration of 180 days

## S3 Intelligent-Tiering
Small monthly monitoring and auto-tiering fee. Moves objects automatically between Access Tiers based on usage. No retrieval cost

- *Frequent Access tier (automatic)*: default tier
- *Infrequent Access tier (automatic)*: objects not access for 30 days
- *Archive Instant Access tier (automatic)*: objects not access for 90 days
- *Archive Access tier (optional)*: configurable from 90 days to 700+ days
- *Deep Archive Access tier (optional)*: configurable from 180 days to 700+ days

![[S3 Storage Classes image.png]]

![[S3 storage classes pricing.png]]

## S3 Express One Zone
An unconventional storage class.

 - High performance, *Single AZ* storage class
 - Objects stored in **Directory Bucket** (bucket in a single AZ)
 - Handle 100,000s requests per second with *single-digit* millisecond latency
 - Up to 10x better performance than S3 standard (50% lower cost)
 - Use case: latency-sensitive apps, AI&ML training, financial modeling...