Stands for "Elastic MapReduce"

EMR helps creating Hadoop clusters (big data) to analyze and process vast amount of data
- Clusters can be made of hundreds of EC2 instances
- It comes bundled with Apache Spark, HBase, Presto, Flink...
- It takes care of all the provisioning and configuration
- Auto-scaling integrated with Spot instances

Use cases: data processing, machine learning, web indexing, big data...


### Node Types & Purchasing
- Master node: Manage the cluster, coordinate, manage health - long running
- Core node: Run tasks, and store data - long running
- Task node (optional): Just to run tasks - usually Spot

**Purchasing**
- On-demand: reliable
- Reserved (min 1 year): cost savings
- Spot: cheaper, less reliable


Can have long-running cluster, or transient (temporary) cluster

