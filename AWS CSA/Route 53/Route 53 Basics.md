A highly available, scalable, fully managed and *Authoritative* DNS
	Authoritative: The customer (you) can update the DNS records

- It is also a Domain Registrar
- Ability to check the health of your resources
- The only AWS service which provides 100% availability SLA

### Hosted Zones
A container for records that define how to route traffic to a domain and its subdomains. There are two types: public and private

- Public hosted zones contains records that specify how to route traffic on Internet
- Private hosted zones only route within one or more VPC

## CNAME vs Alias
**CNAME**:
- Points a hostname to any other hostname
- Only for non-root domain
**ALIAS**:
- Points hostname to an AWS resource (lb-1-23.elb.amazonaws.com)
- Works for root domain and non-root domain
- Free of charge
- Native health check
- You can't set TTL
- **You cannot set an ALIAS record for an EC2 DNS name**
- It only supports A and AAAA record types

> Zone Apex: The top node of a DNS namespace (like nexonet.space)

# Hybrid DNS & Resolver

Route 53 Resolver is the main component that you create while using Route 53.

When you want to connect your on-premise DNS server to Route 53, you need a *Resolver Inbound Endpoint*. This resolver endpoint will talk to main resolver.