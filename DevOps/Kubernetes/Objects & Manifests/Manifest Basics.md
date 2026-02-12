## apiVersion
Version 

## kind
Shows what kind of object we will create. Can be Service, Pod, Deployment etc. (capital)
- **ResourceQuote**: You can specify a quote for a specific *namespace*
## metadata
Custom metadata you can put like name and labels
### namespace
You can specify namespace that the object will be created in
## spec
Specifications of the object. 

### Resource Limiting
You can specify max resources.\
> **Milicore of CPU**: 1 CPU core = 1000 milicore

![[ResourceQuota]]