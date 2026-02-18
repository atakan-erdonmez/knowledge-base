Based on PostgreSQL, but not for OLTP

It's OLAP - online analytical processing (analytics and data warehousing). 10x better performance, scales to PBs of data

- Columnar storage (instead of row-based) & parallel query engine
- Two modes: provisioned cluster and serverless cluster 
- Integrates with BI tools such as Quicksight or Tableu

## Snapshots
Has multi-AZ mode for some clusters
- You can restore a snapshot into a new cluster
- Automated (every 8 hours, every 5GB, or on a schedule) or manual retainment

## Redshift Spectrum
Query data that is already in S3 without loading it. The query is then submitted to thousands of Redshift Spectrum notes