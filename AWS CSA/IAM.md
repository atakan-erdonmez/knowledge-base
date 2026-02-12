Identity and Access management, Global service

You can use groups. One user can be in multiple groups. Groups can't include other groups
## IAM Policies Structure

**Consists of**
- Version: policy language version
- Id: ID for the policy (optional)
- Statement: one or more individual statements (required)
**Statements consists of**
- Sid: Statement ID (optional)
- Effect: Allow or deny
- Principal: account/user/role to which this policy applies to
- Action: list of actions this policy allows or denies
- Resource: list of resources which the actions applies to
- Condition: (optional)

## Users, Groups, Policies
You can change these in in IAM as well as Password settings

## Root user security details

You can access it via signing in with root and clicking top right corner, then "security credentials"


## Access Keys, CLI, SDK
Management console: Web interface
SDK: AWS Software development kit

You use access keys to access CLI and SDK


# CLI Config
use `aws configure` and put your region and access keys. Now you can access AWS resources with CLI.
**THIS SHOULD NEVER BE DONE** due to security

Access keys are a way to access your AWS. However, since the access keys are stored as plain-text, it is not a good practice security-wise

# IAM Role
These are just like users, but for services instead of actual people.

You put an IAM role to the EC2 instance for example, and permissions work on that IAM role