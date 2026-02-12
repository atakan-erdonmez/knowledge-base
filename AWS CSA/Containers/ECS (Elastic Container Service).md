## EC2 Launch Type
Launch ECS Tasks on ECS Clusters

In this launch type, you must provision and maintain the infra. Your ECS/ECS Cluster will have special EC2 instances that each has ECS agent.


## Fargate Launch Type
Fargate is serverless container solution. In this type, you don't provision the infrastructure, it is serverless. You just create tasks definitions, AWS runs ECS tasks based on resources

## ECS Integrations
#### EC2 Instance Profile 
> EC2 launch type only

- Used by ECS agent, makes API calls to ECS service
- Send logs to CloudWatch, pull Docker image from ECR

#### ECS Task Role
- Allows each task to have a specific role
- Use different roles for the different ECS services you run
- Task role is defined in the task definition

## Load Balancer Integration
- ALB is supported for most use cases
- NLB recommended for only high throughput/performance

## Data Volumes (EFS)
You can mount EFS onto ECS tasks. Works with EC2 and Fargate
- Use cases: Persistent multi-az shared storage
- S3 cannot be mounted as filesystem