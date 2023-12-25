# pyspark-emr-optimization

This check list can be used as the starting point for optimizing and troubleshooting bottlenecks in EMR Spark workloads. There are some prerequisites which are required before doing this task. 

## Prerequisites: 

1. [Anatomy of Spark application](https://luminousmen.com/post/spark-anatomy-of-spark-application?source=post_page-----ca4faff40d45--------------------------------)
2. [Deep understanding of Spark Query Plans - how spark operates under the hood](https://dzone.com/articles/reading-spark-query-plans)
3. [How to read and analyze spark DAG from different perspectives](https://dzone.com/articles/reading-spark-dags)
4. [How to use Spark Web UI (History Server UI) for debugging, inspecting and identifying bottleneck](https://spark.apache.org/docs/3.1.1/web-ui.html)
5. AWS EMR Architecture
   
## Check List:

1. **spark.sql.shuffle.partitions**: The default spark.sql.shuffle.partitions=200 does not utilize all the cluster cores and distribute the workload evenly when the **stage input data size > 20GB**. Watch this great talk https://www.youtube.com/watch?v=_ArCesElWp8&t=4512s  by Daniel Tom - how to tune this configuration **spark.sql.shuffle.partitions**
2. **executor-memory, executor-core and num-executor**: Based on cluster configuration how to set these configurations - Use this article https://spoddutur.github.io/spark-notes/distribution_of_executors_cores_and_memory_for_spark_application.html
3. Writing the output files to s3 taking long time, then uses3-dist-cp to copy your data back to S3. If EMR cluster is missing the s3-dist-cp command you have to include Hadoop in your create-cluster command. example: --applications Name=Hadoop Name=Spark
4.    Persist the Dataframe which are being used multiple times. This will reduce the read time.
5. [SPARK OPTIMIZATION TECHNIQUES in page 15](docs/databricks_spark_ui.pdf)
6. [Basics of Apache Spark Configuration Settings](https://towardsdatascience.com/basics-of-apache-spark-configuration-settings-ca4faff40d45)
7. [Spark Jargon for Starters](https://mageswaran1989.medium.com/spark-jargon-for-starters-af1fd8117ada)
8. [Apache Spark Performance Tuning and Optimizations for Big Datasets](https://mageswaran1989.medium.com/spark-optimizations-for-advanced-users-spark-cheat-sheet-d74464618c20)
9. [EMR Best Practices](https://aws.github.io/aws-emr-best-practices/applications/spark/best_practices/)
10. [Best practices to optimize data access performance from Amazon EMR and AWS Glue to Amazon S3](https://aws.amazon.com/blogs/big-data/best-practices-to-optimize-data-access-performance-from-amazon-emr-and-aws-glue-to-amazon-s3/)

