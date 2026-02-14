It is a way for clients to talk to AWS resources. They access the REST API, which then proxies to AWS resources.

Lambda + API Gateway: No infrastructure
- Support for the WebSocket protocol
- Handle different environments, API versions, and security
- Transform and validate requests and responses

## Integration
### Lambda Function
- Invoke functions
- Easy way to expose REST API backed by AWS Lambda
### HTTP
- Expose HTTP endpoints in the backend
- Example: internal HTTP API on premise, ALB...
- Why? Add rate limiting, caching, user auth, API keys...
### AWS Service
- Expose any AWS API through the API Gateway
- Example: start an AWS Step Function workflow, post a message to SQS