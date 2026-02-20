It is like a search engine to query logs. Uses SQL-like language. 

## Container Insights
- Collect, aggregate, summarize metrics and logs from containers. 
- Works on ECS, EKS, Kubernetes on EC2, and Fargate.
- In EKS and Kubernetes, CloudWatch Insights uses a containerized version of CloudWatch agent to discover containers

## Lambda Insights
- Monitoring and troubleshooting solution for serverless applications running on AWS Lambda
- Collects, aggregates, and summarizes system -level metrics including CPU time, memory, disk, and network
- Collects, aggregates, and summarizes diagnostic information such as cold starts and Lambda worker shutdowns
- Lambda Insights is provided as a Lambda Layer
## Contributor Insights
Analyze log data and create time series that display contributor data. See metrics about the top-N contributors
- Works for any AWS-generated logs (VPC, DNS, etc..)
- This helps you find top talkers and understand who or what is impacting system performance
- For example, you can find bad hosts, identify the heaviest network users, or find the URLs that generate the most error

## Application Insights
Provides automated dashboards that show potential problems with monitored applications, to help isolate ongoing issues

- Your applications run on Amazon EC2 Instances with select technologies only (Java, .NET, Microsoft IIS Web Server, databases…)
- You can use other AWS resources such as Amazon EBS, RDS, ELB, ASG, Lambda, SQS, DynamoDB, S3 bucket, ECS, EKS, SNS, API Gateway…
- Enhanced visibility into your application health to reduce the time it will take you to troubleshoot and repair your applications, powered by SageMaker