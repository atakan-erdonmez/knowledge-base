![[sns+sqs.png]]

When you want a message to be sent to multiple SQS queues. So you push once to SNS topic, and subscribe SQS queues.

- Fully decoupled, no data loss
- SQS allows for: data persistence, delayed processing and retries of work
- Ability to add more SQS subscribers
- SQS should allow SNS to write
- Cross-Region Delivery: works with SQS queues in other regions