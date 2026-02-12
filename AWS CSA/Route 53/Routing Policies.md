Supports following policies:
- Simple
- Weighted
- Failover
- Latency-based
- Geolocation
- Multi-value Answer
- Geoproximity
## Single
Generally, route traffic to a single resource

Can specify multiple values in the same record. If multiple values are returned, a random one is chosen by the *client*

## Weighted
Control the % of the requests that go to each specific resource
- DNS records must have the same name and type
- Can be associated with Health Checks

## Latency
Redirect to the resource that has the least latency close to use. It is helpful when latency is a priority

## Failover (Active-Passive)
There is a primary health check (mandatory) and a secondary health check. They point to different endpoints. If primary health check fails, it failovers to secondary

## Geolocation
The routing is based on user location. You can specify different endpoints for different locations. Also, you will have a *default* location for default option

## Geoproximity
Route based on location of users *and* resources. Ability to shift more traffic to resources based on defined bias
- To expand (1 to 99) - more traffic to the resource
- To shrink (-1 to -99) - less traffic to the resource

Resource can be both AWS and non-AWS (you must use Route 53 Traffic Flow (advanced ) to use this feature)

## IP-based
You provide a list of CIDR for your clients and corresponding endpoints
Use cases: optimize performance, reduce network cost...

## Multi-value
Used when routing traffic to multiple resource. You send multiple A records, and client chooses randomly. 
> The difference between standard routing, is that multi-value enables health checks