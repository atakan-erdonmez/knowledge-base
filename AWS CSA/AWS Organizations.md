It is a global service to manage multiple AWS accounts. There is the main management account and multiple member accounts. A member account can only be a part of one organization. It can cause some discounts and saving plans. 


## Hierarchy
There is Root OU (Root Organization Unit), which includes the Management Account. 

Under management, you can create OUs and subOUs.

![[Organization Example OU.png]]
## Advantages
- Multi account for easier management & security
- Use tagging standards for billing purposes
- Enable CloudTrail and CloudWatch on multiple accounts
- Establish Cross Account Roles for admin purposes

#### Security: Service Control Policies (SCP)
It is a special IAM policy applied to OU or Accounts to restrict Users and Roles. *They don't apply to management account.* Must have an explicit allow, so least privilege.

> If parent OU has AllowAll, but a child account only has AllowEC2, parent permissions don't apply. It will only accsess EC2


## Tag Policies
Defines who can use what tags on resources.