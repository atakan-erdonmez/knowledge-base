- Aurora is a proprietary technology from AWS (not open sourced)
- Postgres and MySQL are both supported as Aurora DB (that means your drivers will work as if Aurora was a Postgres or MySQL database)
- Aurora is “AWS cloud optimized” and claims 5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS
- Aurora storage automatically grows in increments of 10GB, up to 128 TB.
- Aurora can have up to 15 replicas and the replication process is faster than MySQL (sub 10 ms replica lag)
- Failover in Aurora is instantaneous. It’s HA (High Availability) native. 
- Aurora costs more than RDS (20% more) – but is more efficient

## High Availability and Read Scaling
- 6 copies of your data across 3 AZ:
	- 4 copies out of 6 needed for writes
	- 3 copies out of 6 need for reads
	- Self healing with peer-to-peer replication
	- Storage is striped across 100s of volumes

- One Aurora Instance takes writes (master)
- Automated failover for master in less than 30 seconds
- Master + up to 15 Aurora Read Replicas serve reads
- Support for Cross Region Replication


## Endpoints
There are writer and reader endpoint.

**Writer endpoint:**
- It will point to the master, which is the only DB that can write to storage
- Even when master fails over, client will connect to writer endpoint and will be redirected to the new master, providing failover 

> **ONLY THE MASTER CAN WRITE**


**Reader endpoint:**
- Read Replicas can auto scale, and it can be hard for apps to track which replica is where
- Reader endpoint act as a connection load balancer, connecting all read replicas

## Features
- Automatic fail-over
- Backup and Recovery
- Isolation and security
- Industry compliance
- Push-button scaling
- Automated Patching with Zero Downtime
- Advanced Monitoring
- Routine Maintenance
- Backtrack: restore data at any point of time without using backups

# Advanced Features
## Auto Scaling
You can set up auto scaling, so read replicas will be scaled accordingly. Reader endpoint will extend to cover newly generated replicas.
## Custom Endpoints
You create a custom endpoint to cover some replicas. Like if you have 2 stronger instances, you can redirect them to your custom endpoint for running analytical queries
## Serverless 
Automated database instantiation. Good for infrequent, intermittent or unpredictable workload
- No capacity planning needed
- Pay per second, can be more cost-effective
## Global Aurora
**Aurora Cross Region Read Replicas:**
- Useful for disaster recovery
- Simple to put in place
**Aurora Global Database (recommended)**:
- 1 Primary region (read/write)
- Has multi-region database
- Up to 10 secondary (read-only) regions, replication lag is **less than 1 second**
- Up to 16 Read Replicas per secondary region
- Helps for decreasing latency
- Promoting another region (for disaster recovery) has an RTO of <1 minute
- **Typical cross-region replication takes less than 1 second**


## Aurora Database Cloning
It is used to create a new cluster that initially shares the same data, but a separate and independent volume.

- Create a new Aurora DB cluster from an existing one
- Faster than snapshot & restore, because it uses copy-on-write protocol where only writes happen when there are changes