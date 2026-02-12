When you start deploying multiple applications, they will need to communicate each other.

2 types of communication:
**1- Synchronous:** Application to application
- It can be problematic in sudden spikes of traffic
- If too much spike, it is better to *decouple* your apps 
**2- Asynchronous / Event Based:** Application to queue to application
- SQS: Queue Model
- SNS: pub/sub model
- Kinesis: Real-time streaming model