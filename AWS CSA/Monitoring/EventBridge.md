It is a scheduling system. You can schedule events based on time, or an event pattern.

It can run a cron job every hour, or it can react to an event (IAM Root user sign in for example), and trigger a function, like Lambda or SQS message

It is the default bus. You have resources that you get data from, and destinations to run actions. You can also use 3rd party partners' event bus


## Schema Registry
EventBridge can analyze the events in the bus and infer the schema

Schema Registry allows you to generate code for your application, that will know in advance how data is structured in the event bus