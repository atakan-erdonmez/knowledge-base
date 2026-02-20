Helps with auditing and recording compliance of your AWS resource. It is a fully  managed service that acts as a **resource inventory**, **configuration history**, and **compliance engine** for your AWS environment.

Questions that can be solved by AWS Config:
- Is there unrestricted SSH access to my security groups?
- Do my buckets have any public access?
- How has my ALB configuration changed over time?

### Config Rules
You can use AWS managed config rules (over 140), or make custom rules defined in Lambda
- Ex: evaluate if each EBS disk is of type gp2
- Ex: evaluate if each EC2 instance is t2.micro

> [!warning]
> Config Rules do not prevent actions from happening. It is just for compliance


## Remediations
These are specific actions that follows detection to fix the issue.

- **How it works:** When an AWS Config Rule (like one checking for open port 22) identifies a non-compliant resource, it can trigger a **Remediation Action**.

- **The Engine:** These actions are typically powered by **AWS Systems Manager (SSM) Automation documents**. For example, a document can be configured to automatically remove the `0.0.0.0/0` rule from a Security Group the moment it is detected.

- **Execution:** You can set these to run **automatically** (fixing the issue instantly) or **manually** (requiring a click from an admin).