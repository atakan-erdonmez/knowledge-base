Edge Function: A code that runs close to users to minimize latency. You run it on CloudFront. You have these 2 options 
#### CloudFront Functions
- Lightweight functions written in JavaScript
- For high-scale, latency-sensitive CDN customizations
- Sub-ms startup times, millions of request/second
- Used to change Viewer requests and responses in CDN
#### Lambda@Edge
- Lambda functions written in NodeJS or Python
- Scales to 1000s of request/second
- Can change both viewer and origin requests and responses in CDN


## Comparison

| Feature                        | CloudFront Functions                      | Lambda@Edge                                      |
| ------------------------------ | ----------------------------------------- | ------------------------------------------------ |
| **Runtime Support**            | JavaScript                                | Node.js, Python                                  |
| **# of Requests**              | Millions of requests per second           | Thousands of requests per second                 |
| **CloudFront Triggers**        | Viewer Request/Response                   | Viewer Request/Response, Origin Request/Response |
| **Max. Execution Time**        | < 1 ms                                    | 5 – 10 seconds                                   |
| **Max. Memory**                | 2 MB                                      | 128 MB up to 10 GB                               |
| **Total Package Size**         | 10 KB                                     | 1 MB – 50 MB                                     |
| **Network/File System Access** | No                                        | Yes                                              |
| **Access to Request Body**     | No                                        | Yes                                              |
| **Pricing**                    | Free tier available, 1/6th price of @Edge | No free tier, charged per request & duration     |
## Use Cases
### CloudFront Functions

- Cache key normalization
    - Transform request attributes (headers, cookies, query strings, URL) to create an optimal Cache Key
- Header manipulation
    - Insert/modify/delete HTTP headers in the request or response
- URL rewrites or redirects
- Request authentication & authorization
    - Create and validate user-generated tokens (e.g., JWT) to allow/deny requests

---

## Lambda@Edge

- Longer execution time (several ms)
- Adjustable CPU or memory
- Your code depends on a 3rd libraries (e.g., AWS SDK to access other AWS services)
- Network access to use external services for processing
- File system access or access to the body of HTTP requests