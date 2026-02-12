It is a blueprint of deploying an application. It is great for developers.
- It uses all components like EC2, ASG, ELB, RDS to configure an environment
- It is a managed service, automatically handles provisioning, load balancing, scaling, health monitoring...
- It is a free service, you will pay for the deployed components

## Components
- Application: Collection of components (environments, versions, configurations..)
- Application Version: An iteration of the application code
- Environment: Collection of resource running an app version. Has multiple tiers, and you can create multiple envs

> It has *Web server tier* and *worker tier*.