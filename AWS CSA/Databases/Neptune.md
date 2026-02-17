Fully managed **graph** database

### What is Graph Database?
It is like a network of information:
- Like a social network, users have friends, posts have comments, comments have likes from users ...
- Everything is interconnected



- Highly available across 3AZ, up to 15 read replicas
- Optimized for these complex and hard queries
- Can store up to billions of relations and query the graph with ms latency
- Gread for knowledge graphs (Wikipedia), fraud detection, recommendation engines, social networking...

## Neptune Streams
Real-time ordered sequence of every change
- Changes are available immediately after writing
- No duplicates, strict order
- Accessible with REST API

Use cases:
- Send notifications when changes made
- Make your graph sync to other data stores (S3, OpenSearch..)
- Replicate data across regions in Neptune