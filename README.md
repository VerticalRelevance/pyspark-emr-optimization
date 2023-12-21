# pyspark-emr-optimization

This check list can be used as the starting point for optimizing and troubleshooting bottlenecks in EMR Spark workloads. There are some prerequisites which are required before doing this task. 

## Prerequisites: 

1. Spark Architecture and how does it integrate with Hadoop YARN. 
2. Deep understanding of Spark Query Plans - how spark operates under the hood.
3. How to read and analyze spark DAG from different perspectives. 
4. How to use Spark Web UI (History Server UI) to identify the bottleneck.
5. AWS EMR Architecture
   
## Check List:

1. **spark.sql.shuffle.partitions**: The default spark.sql.shuffle.partitions=200 does not utilize all the cluster cores and distribute the workload evenly when the **stage input data size > 20GB**. Watch this great talk https://www.youtube.com/watch?v=_ArCesElWp8&t=4512s  by Daniel Tom - how to tune this configuration **spark.sql.shuffle.partitions**
2. **executor-memory, executor-core and num-executor**: Based on cluster configuration how to set these configurations - Use this article https://spoddutur.github.io/spark-notes/distribution_of_executors_cores_and_memory_for_spark_application.html
3. Writing the output files to s3 taking long time, then uses3-dist-cp to copy your data back to S3. If EMR cluster is missing the s3-dist-cp command you have to include Hadoop in your create-cluster command. example: --applications Name=Hadoop Name=Spark
4.    Persist the Dataframe which are being used multiple times. This will reduce the read time.

