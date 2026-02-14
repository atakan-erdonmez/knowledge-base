Give users an identity to interact with our web or mobile application

### Cognito User Pools
- Sign in functionality for app users
- Integrate with API Gateway & ALB
### Cognito Identity Pools (Federated Identity)
- Provide AWS credentials to users so they can access AWS resources directly
- Integrate with Cognito User Pools as an identity provider

**Cognito vs IAM:** 'hundreds of users', 'mobile users', 'authenticate with SAML'


## Cognito User Pools (CUP) - User Features

Create a serverless database of user for your web & mobile apps

Simple login with username/password. Ability to reset password, email & phone verification, MFA, featured identities like Facebook, google

## Cognito Identity Pools (Federated Identities)

Get identities for users so they obtain temporary AWS credentials

- Users can access AWS services directly or through API Gateway.
- IAM policies applied to credentials defined in Cognito. 
- Customizable based on user_id for fine-grained control. 
- Default IAM roles for authenticated and guest users