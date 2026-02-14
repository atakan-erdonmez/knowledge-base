It is a fully managed, highly available NoSQL database. Distributed, scales to massive workloads, replication with multiple AZ.

- Fast and consistent performance (single digit ms)
- Low cost and auto scaling
- No maintenance or patching, always available
- Standard and Infrequent Access (IA) data

It is made of *tables*. Each table has a primary key, and can have an infinite number of rows. Each item has attributes, which can be increased over time. Max item size=400kb


## Read/Write Capacity Modes
### Provisioned Mode (default)
Specify read-writes beforehand. Pay for provisioned RCU (Read Capacity Units) and WCU (Write Capacity Units). Possibility to add auto-scaling for RCU&WCU

### On-Demand Mode
Automatic scaling. Much more expensive. Great for *unpredictable workloads* and *sudden spikes*



## Features
### DynamoDB Accelerator (DAX)
Fully-managed, highly available, seamless in-memory cache. Help solve read congestion, *microsecond latency*. Doesn't require application logic modification. TTL=5 min by default

### Stream Processing
Ordered stream of item-level modifications (create/update/delete) in a table.
Use cases:
- React to changes in real time (welcome email to users)
- Real-time usage analytics
- Insert into derivative tables
- Implement cross-region replication
- Invoke AWS Lambda on changes to you DynamoDB

### Global Tables
It means that tables that are global will have two-way replication. This makes DynamoDB table accessible with low latency in multiple regions. 
- Active-Active replication
- Applications can read and write to the table in any region
- Must enable DynamoDB Streams as a pre-requisite

### TTL
Automatically delete items after an expiry timestamp

### Backups

**Continuous backups using point-in-time recovery (PITR)**
- Optionally enabled for last 35 days
- Point-in-time recovery to any time within backup windows
	- Backup creates a new table 

**On-demand backups**
- Full backups for long-term retention, until explicitly deleted
- Doesn't affect performance or latency
- Can be configured with AWS Backup (enable cross-region copy)
- Recovery creates a new table

### S3 Integration
**Export to S3 (with PITR)**
- Works for any point-of-time in last 35 days
- No affect on read capacity
- Retain snapshots, perform data analysis
**Import from S3**
- Import CSV, DynamoDB JSON or ION format
- No affect on write capacity
- Creates a new table