Flink (Java, Scala, SQL): A framework for processing data streams

Run any Apache Flink application on a managed cluster on AWS
- Provision compute resources, parallel computation, automatic scaling
- Application backups
- Use any Apache Flink programming features
- Important: Flink does not read from Amazon Data Firehose
	- It reads from Kinesis Data Streams, Amazon MSK (Apache Kafka)