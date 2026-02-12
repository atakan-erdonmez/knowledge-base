Normally, in direct integration, a service sends one message to many receivers.
In pub/sub system (publish/subscribe), a service publishes into SNS topic, which has multiple subscribers
![[SNS1.png]]

In SNS:
- The 'event producer' only sends message to one SNS topic
- You can have as many 'event receivers' as you want to list SNS topic notifications
- Each subscriber will get all messages (filtering also available)
- Up to 12.000.000 subscription per topic and 100.000 topic limit

## How to Publish

**Topic Publish (using SDK)**
1. Create a topic
2. Create a subscription (or many)
3. Publish the topic

**Direct Publish (for mobile apps SDK)**
1. Create a platform application
2. Create a platform endpoint
3. Publish to platform endpoint
-  Works with Google GCM, Apple APNS, Amazon ADM

# Subscription Services
- Amazon Kinesis Data Firehose
- Amazon SQS
- AWS Lambda
- Email
- Email-JSON
- HTTP
- HTTPS
- Platform application endpoint
- SMS