In real-life, the load on your websites and application can change
In the cloud, you can create and get rid of servers very quickly

The goal of an Auto Scaling Group (ASG) is to: 
- Scale out (add EC2 instances) to match an increased load
- Scale in (remove EC2 instances) to match a decreased load
- Ensure we have a minimum and a maximum number of EC2 instances running
- Automatically register new instances to a load balancer
- Re-create an EC2 instance in case a previous one is terminated (ex: if unhealthy)
- ASG are free (you only pay for the underlying EC2 instances)

> It can talk with Load Balancer and replace any unhealthy EC2 instances automatically.

> It also can add new EC2 instances to the Load Balancer automatically

## Launch Template
- A Launch Template (older “Launch Configurations” are deprecated) 
	- AMI + Instance Type
	- EC2 User Data
	- EBS Volumes
	- Security Groups
	- SSH Key Pair
	- IAM Roles for your EC2 Instance
	- Network + Subnets Information
	- Load Balancer Information
- Min Size / Max Size / Initial Capacity
- Scaling Policies

# Scaling Policies

### Dynamic Scaling

##### - Target Tracking Scaling
- Simple to set up
- Example: I want the average ASG CPU to stay around at 40%
##### - Simple / Step Scaling
- When a CloudWatch alarm is triggered (example CPU > 70%), then add 2 units
- When a CloudWatch alarm is triggered (example CPU < 30%), then remove 1

### Scheduled Scaling
- Anticipate a scaling based on known usage patterns
- Example: increase the min capacity to 10 at 5 pm on Fridays
### Predictive Scaling
- Continuously forecast load and schedule scaling ahead. Automatically guess the possible load


### Good metrics to scale on
- CPU Utilization
- RequestCountPerTarget
- Average Network In / Out
- Any custom metric (that you push using CloudWatch)