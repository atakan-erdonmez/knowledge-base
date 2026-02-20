
Provides governance, compliance and audit for your AWS Account, enabled by default.

- Get an history of events, API calls made within your AWS account by:
	- Console
	- SDK
	- CLI
	- AWS Services 
- You can put logs from CloudTrail into CloudWatch Logs or S3

## Event Types

#### Management Events
Operations that are performed on resources in your AWS account. Examples:
	- Configuring security (IAM AttachRolePolicy)
	- Configuring rules for routing data (Amazon EC2 CreateSubnet)
	- Setting up logging (AWS CloudTrail CreateTrail)

- By Default, trails are configured to log management events.
- You can separate **Read Events** (no modification on resources) or **Write Events** (may modify resources)


#### Data Events
By defaults, data events are not logged (because of high volume)
- Amazon S3 object-level activity (ex: GetObject, DeleteObject, PutObject): can separate Read and Write Events
- AWS Lambda function execution activity (the Invoke API)

#### CloudTrail Insights Events
It analyzes your account to detect unusual activity, like inaccurate resource provisioning, hitting service limits, bursts of IAM actions etc.

CloudTrail Insights analyzes normal management events to create a baseline. And then **continuously analyzes write events** to detect unusual patterns
- Anomalies appear in CloudTrail console
- Event is sent to S3
- An EventBridge event is generated (for automation)


## Event Retention
Events are stored for 90 days in CloudTrail.
To keep them beyond this point, log them to S3 and use Athena to analyze