It is Layer 4 LB
- Forward TCP & UDP traffic
- Ultra-low latency, handle millions of request

-> NLB has *one static IP per AZ* and supports assigning Elastic IP

### Target Groups
- EC2 instances
- IP addresses - must be private IPs
- Application Load Balancer
- Health Checks support the *TCP, HTTP, and HTTPS protocol*