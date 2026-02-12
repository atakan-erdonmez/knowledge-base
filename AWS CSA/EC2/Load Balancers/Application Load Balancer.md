It is layer 7. Load balancing to multiple HTTP applications across machines (target group).
- It can load balance to multiple apps on same machine (containers)
- Supports HTTP/2 and WebSocket and support redirects
- They are great fit for microservices & container-based applications (docker & Amazon ECS)
### Target Groups
- EC2 instances (can be managed by an Auto Scaling Group) - HTTP
- ECS tasks (managed by ECS itself)  - HTTP
- Lambda functions - HTTP request is translated into a JSON event
- IP Addresses - must be private IPs