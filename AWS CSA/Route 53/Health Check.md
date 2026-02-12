HTTP Health Checks are only for public resources. It is used for **Automated DNS Failover**.

3 types:
- Health check that monitor an endpoint (application, server...)
- Health check that monitor other health checks (Calculated health checks)
- Health checks that monitor CloudWatch alarms (full control) - throttles of DynamoDB, alarms on RDS, custom metrics etc
# Health Check - Endpoint
About 15 global health checkers will check the endpoint health.
- Healthy/Unhealthy Threshold - 3 (default)
- Interval - 30 sec (can set to 10 sec - higher cost)
- Supported: HTTP, HTTPS and TCP
- If > 18% success , it is healthy

# Calculated Health Checks
Combine the results of multiple Health Checks into a single Health Check
- There are Child health checks, monitored by Parent health check
- Can monitor up to 256 Child health check

# Health Checks - Private Hosted Zones
Route 53 health checkers are outside the VPC, they can't access private endpoints

In order to achieve that, you can create a CloudWatch metric and associate a CloudWatch alarm, then create a Health Check that checks the alarm itself