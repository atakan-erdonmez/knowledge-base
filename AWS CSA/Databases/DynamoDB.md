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
- Invoke AWS Lambda on changes to you DynaoDB