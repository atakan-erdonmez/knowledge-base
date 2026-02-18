When you have an app with multiple edge locations, you can use Global Accelerator. It works by giving 2 anycast IP addresses to all edge locations.

- So when you put the same IP, you will be directed to the closest edge location
- 2 IP is given for high availability


- It works with Elastic IP, EC2, ALB, NLB, public or private
- Consistent performance
	- Intelligent routing to lowest latency and fat regional failover
	- No issue with client cache (because IP doesn't change)
	- Internal AWS network
- Health Checks on your applications with automatic failover
- Increased security with integrated DDoS protection and only 2 external IP to be whitelisted


# Global Accelerator vs CloudFront
CloudFront is a CDN. It caches and distributes from edge location.
Global Accelerator is just redirects packages inside the AWS network. So instead of using the Internet for the whole path, you incorporate AWS internal network for speed and latency.


- They both use the AWS global network and its edge locations around the world
- Both services integrate with AWS Shield for DDoS protection

**CloudFront**
- Improves performance for both cacheable content (such as images and videos)
- Dynamic content (such as API acceleration and dynamic site delivery)
- Content is served at the edge

**Global Accelerator**
- Improves performance for a wide range of applications over TCP or UDP
- Proxying packets at the edge to applications running in one or more AWS Regions.
- Good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP
- Good for HTTP use cases that require static IP addresses

