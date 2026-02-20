It provides metrics for every service in AWS. Metric is a variable to monitor like CPU utilization, NetworkIN etc.

- Metrics belong to namespaces
- Dimension is an attribute of metric (instance id, environment...)

> Standard monitoring is every 5 minutes, detailed monitoring every 1 minute
## Metric Stream
Continuously stream CloudWatch metrics to a destination, with near-real-time delivery and low latency.
- Kinesis Data Firehose (and then its destinations)
- 3rd party: Datadog, Dynatrace, New Relic, Splunk, Sumo Logic...