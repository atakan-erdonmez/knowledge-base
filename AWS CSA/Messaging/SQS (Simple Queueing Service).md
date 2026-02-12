Producer sends messages to SQS, consumers poll the messages from SQS
![[SQS.png]]
It is a fully managed service, used to **decouple applications.**

# Standard Queues

**Attributes:**
- Unlimited throughput, unlimited messages in queue
- Default retention of messages: 4 days to maximum 14 days
- Low latency (<10ms on publish and receive)
- Limitation of 1024KB per message

- Can have duplicate messages (at least once delivery, occasionally)
- Can have out of order messages (best effort ordering)

#### Producing Messages
Producers creates messages using SDK (Software Development Kits) to send to SQS. SendMessage API is used. The message is persisted in SQS until deleted by consumer.

#### Consuming Messages
Poll SQS for message, up to 10 messages at a time. Then process the messages and delete form the queue using DeleteMessage API.


### Message Visibility Timeout
After a message is polled by a consumer, it becomes *invisible*. 
- By default, timeout is 30 seconds. Message needs to be processed in 30 sec
- After the timeout is over, message is visible again

- If a message is not processed in the time, it might be processed twice. Thus, consumer can call ChangeMessageVisibility API to get more time 

> If you set timeout too high, if a consumer crashes, re-processing will take too long. If you set too low, you might get duplicates


### Long Polling
When a consumer requests a message and queue is empty, it can wait for messages, which is called Long Polling.

It decreases API calls to increase efficiency and reduce latency. 1-20 sec


# FIFO Queues
FIFO = First In First Out (ordering of messages)

Producer will send messages in order, consumer will poll them in order.

- Limited throughput: 300msg/s w/o batching, 3000msg/s w/ batching
- Exactly-once send capability (removes duplicates)

