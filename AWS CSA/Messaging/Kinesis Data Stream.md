Collet and store streaming data in **real-time**.
![[Kinesis data stream.png]]

- Retention up to 365 days
- Ability to reprocess (replay) data by consumers
- Data can't be deleted from Kinesis (until it expires)
- Data up to 10MiB (typical use cases is a lot of 'small' real-time data)
- Kinesis Producer Library (KPL) to write an optimized producer app
- Kinesis Client Library (KCL) to write an optimized consumer application

## Capacity Modes
#### Provisioned mode
- Choose number of **shards** (how much throughput)
- Each shard gets 1MB/s in (or 1000 records per second)
- Each shards get 2MB/s out
- Scale manually to increase or decrease shards
- Pay per shard provisioned per hour
#### On-demand mode
- No need to provision or manage capacity
- Default capacity provisioned (4 MB/s in or 4000 records/s)
- Scales automatically based on observed throughput in last 30 days
- Pay per stream hour & data in/our per GB