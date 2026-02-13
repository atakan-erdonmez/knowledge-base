![[data firehose.png]]


> Used to be called "Kinesis Data Firehose"

A fully managed service
- Amazon Redshift / Amazon S3 / Amazon OpenSearch
- 3rd party: Splunk / MongoDB / Datadog / NewRelic
- Custom HTTP endpoint

- Automatic scaling, serverless, pay for what you use
- **Near real-time** with buffering capability based on size/time 
- Supports CSV, JSON, Parquet, Avro, Raw Text, Binary data 
- Custom data transformation using Lambda

# Kinesis Data Stream vs Amazon Data Firehose


| Kinesis Data Stream          | Amazon Data Firehose                                 |
| ---------------------------- | ---------------------------------------------------- |
| Streaming data collection    | Load streaming data into S3, Redshift, 3rd party ... |
| Producer & consumer code     | Fully managed                                        |
| Real-time                    | Near real-time                                       |
| Provisioned / On-demand mode | Automatic scaling                                    |
| Data storage up to 365 days  | No data storage                                      |
| Replay capability            | No replay                                            |
