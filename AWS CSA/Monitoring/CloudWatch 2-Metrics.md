It provides metrics for every service in AWS. Metric is a variable to monitor like CPU utilization, NetworkIN etc.

- Metrics belong to namespaces
- Dimension is an attribute of metric (instance id, environment...)

> Standard monitoring is every 5 minutes, detailed monitoring every 1 minute
## Metric Stream
Continuously stream CloudWatch metrics to a destination, with near-real-time delivery and low latency.
- Kinesis Data Firehose (and then its destinations)
- 3rd party: Datadog, Dynatrace, New Relic, Splunk, Sumo Logic...

## Metrics
Exist both in standard and detailed monitoring:

|**Category**|**Metric Name**|**What it Tracks**|
|---|---|---|
|**CPU**|`CPUUtilization`|Percentage of allocated CPU being used.|
||`CPUCreditUsage / Balance`|Only for burstable instances (T2, T3, etc.).|
|**Network**|`NetworkIn / NetworkOut`|Total Bytes received/sent on all interfaces.|
||`NetworkPacketsIn / Out`|Total number of packets received/sent.|
|**Disk (Instance Store)**|`DiskReadOps / WriteOps`|I/O operations on ephemeral (local) disks.|
||`DiskReadBytes / WriteBytes`|Data throughput on ephemeral (local) disks.|
|**Status Checks**|`StatusCheckFailed`|Reports if the instance or system is failing.|
||`StatusCheckFailed_Instance`|Failure due to your OS/Configuration.|
||`StatusCheckFailed_System`|Failure due to AWS hardware/power issues.|

Exists only in detailed monitoring:
- **Memory (RAM):** `mem_used_percent`, `mem_available`, etc.
    
- **Disk Utilization:** `disk_used_percent` (how full your actual drive/partition is).
    
- **Swap Usage:** `swap_used`.
    
- **Process Count:** Number of active threads/tasks.