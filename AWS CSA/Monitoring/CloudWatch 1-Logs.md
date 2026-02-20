It is a place to store your application logs. You must first create **log groups**, and inside, multiple **log streams**. You can define log expiration. You can also send logs to:
- S3 (export)
- Kinesis Data Stream
- Amazon Data Firehose
- Lambda
- OpenSearch

### Sources
- SDK, CloudWatch Logs Agent (kinda deprecated), CloudWatch Unified Agent
- Elastic Beanstalk: collection of logs from application
- ECS: collection from containers
- AWS Lambda: collection from function logs
- VPC Flow Logs: VPC specific logs
- API Gateway
- CloudTrail based on filter
- Route53: Log DNS queries

### Logs Insights
It is a querying capability to find logs. It helps visualizing too


## CloudWatch Agents
By default, no logs from EC2 will go to CloudWatch. For that, you need a CloudWatch agent on EC2 to push log files

There are 2 types of agents: Logs Agent (older) and Unified Agent (newer)

##### Logs Agent
- Old version, can only send to CloudWatch logs
##### Unified Agent
- Collect additional system-level metrics like RAM, processes
- Centralized configuration using SSM Parameter store
- Send to CloudWatch Logs