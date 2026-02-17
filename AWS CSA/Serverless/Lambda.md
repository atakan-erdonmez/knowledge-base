| EC2                        | Lambda                                   |
| -------------------------- | ---------------------------------------- |
| Virtual servers            | Virtual functions - no servers to manage |
| Limited by RAM and CPU     | Limited by time - short executions       |
| Continuously running       | Run on-demand                            |
| Scaling means intervention | Scaling is automated                     |

## Advantages
- Easy pricing with pay per request and compute time
- Integrated with whole AWS suite, supports many programming languages
- Easy monitoring with CloudWatch 
- Easy to get more resources per functions (up to 10GB of RAM, increasing ram will increase CPU and network performance)

## Limits
#### Execution
- Memory allocation: 128MB - 10GB (1MB increments)
- Maximum execution time: 900 second (15 minutes)
- Environment variables (4KB)
- Disk capacity - temp space: 512MB to 10GB
- Concurrency executions: 1000 (can be increased)
#### Deployment
- Function deployment size (compressed zip): 50MB
- Size of uncompressed deployment (code + dependencies): 250MB
- /tmp dir can be used

## Concurrency and Throttling
Concurrency limit is 1000 concurrent executions. You can set a "reserved concurrency" (limit) at the function to level to limit this, and it is recommended. This limit applies to all your functions in your account.

Each invocation over the concurrency limit will trigger a "Throttle"

**Cold Start** The initialization delay that occurs when AWS downloads your code and starts a runtime for a new execution environment. This typically happens during the first request after a period of inactivity or when the function scales out to handle more traffic.

**Unreserved Concurrency** The default pool of capacity shared by all functions in an AWS account within a specific region. It allows for flexible scaling, but functions compete for the same resources, meaning a spike in one function can potentially throttle others.

**Reserved Concurrency** A specific amount of capacity set aside for a single function to guarantee it always has execution environments available. It also acts as a hard limit, preventing that function from scaling beyond a certain point and overwhelming downstream resources like databases.

**Provisioned Concurrency** Pre-warmed execution environments that stay initialized and ready to respond immediately to traffic. This feature eliminates cold start latency for the specified capacity in exchange for a consistent hourly cost.

## SnapStart
Normally, a function goes throuth "init -> invoke -> shutdown" and init can take a long time. By pre-initializing the function, you can increase performance.

When you publish a new version, it gets inited and snapshoted for low latency access.

## Network
By default, Lambda functions are out of your VPC (Amazon managed VPC), so it can't access your resources. If you want it in your VPC, you need to define VPC ID, the Subnets and Security Groups.

One of the most common use cases is with [[RDS#RDS Proxy|RDS Proxy]]