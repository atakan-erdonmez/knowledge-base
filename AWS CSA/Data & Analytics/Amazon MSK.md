Managed Streaming for Apache Kafka

It is an alternative to Amazon Kinesis, fully managed Kafka on AWS

- Allows you to create, update, delete clusters
- Creates & manages Kafka broker nodes & Zookeeper nodes for you
- Deploy in VPC, multi-AZ (up to 3 for HA)
- Automatic recovery for common failures
- Stored on EBS volumes

### MSK Serverless
Run Kafka on MSK without managing the capacity. Automatically provision resources and scale


## Kinesis Data Streams vs Amazon MSK

| Kinesis Data Streams      | Amazon MSK                            |
| ------------------------- | ------------------------------------- |
| 1 MB message size limit   | 1MB default, configure for higher     |
| Data streams with shards  | Kafka Topics with Partitions          |
| Shard Splitting & Merging | Can only add partitions to a topic    |
| TLS in-flight encryption  | PLAINTEXT or TLS in-flight encryption |
| KMS at-rest enc           | KMS at-rest enc                       |
[[Kinesis Data Stream]]


### Consumers Example
- Lambda
- Kinesis Data Analytics for Apache Flink
- AWS Glue Streaming ETL Jobs, powered by Apache Spark Streaming
- Applications running on EC2, ECS, EKS