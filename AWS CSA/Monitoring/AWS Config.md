Helps with auditing and recording compliance of your AWS resource.

Questions that can be solved by AWS Config:
- Is there unrestricted SSH access to my security groups?
- Do my buckets have any public access?
- How has my ALB configuration changed over time?

### Config Rules
You can use AWS managed config rules (over 75), or make custom rules defined in Lambda
- Ex: evaluate if each EBS disk is of type gp2
- Ex: evaluate if each EC2 instance is t2.micro

> [!warning]
> Config Rules do not prevent actions from happening. It is just for compliance

