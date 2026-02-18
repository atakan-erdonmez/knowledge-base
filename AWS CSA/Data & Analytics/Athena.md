Serverless query service to analyze data stored in Amazon S3. Uses standard SQL.
- Supports CSV, JSON, ORC, Avro, and Parquet
- $5 per TB of data scanned
- Commonly used with Quicksight for reporting/dashboard

Use cases: BI, analytics, reporting, ELB logs, VPC flow logs, CloudTrail trails ..


## Performance Improvement
Use columnar data for cost-savings (less scan). Apache Parquet or ORC is recommended
- Huge performance improvement
- Use Glue to convert your data to Parquet or ORC
- Compress data for smaller retrievals
- Partition datasets in S3 for easy querying
- Use larger files (128MB>) to increase performance

## Federated Query
Allows you to run SQL queries across data stored in relational, non-relational, object, and custom data sources (AWS or on-premises)
- Uses Data Source Connectors that run on AWS Lambda to run queries