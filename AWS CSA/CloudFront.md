It is the CDN. Improves read performance by caching the content at the edge.

It has multiple origins (sources):
- S3 bucket
	- Distributing files and caching
	- Uploading to S3
	- Secured using Origin Access Control (OAC, which basically controlls the permissions, turning a public access into a public -> OAC -> S3)
- VPC Origin
	- For applications hosted in VPC private subnets
	- ALB/NLB/EC2
- Custom Origin (HTTP)
	- S3 website (enable static S3 website)
	- Any public HTTP backend you want

## ALB or EC2 as an origin
The best way is to connect VPC private subnets to CloudFront. It will use VPC origin.
- This way, you don't have to expose anything on the Internet. CloudFront will use your VPC Origin to connect your Private Subnet

## Geo Restriction
You can restrict based on geolocation. You can use allowlist or blocklist. Country is determined using 3rd party Geo-IP database

## Price Classes
Prices differ between edge locations and total used data.
**Price Classes**:
1. All: all regions, best performance
2. 200: most regions, but excludes most expensive
3. 100: only least expensive regions

# Cache Invalidation
In order to change cached content, it should invalidate. You can wait for TTL or force an entire or partial cache refresh by *CloudFront Invalidation*.
- You can invalidate all files or special paths/prefixes

