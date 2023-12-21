# How to check number of records in each partition

```python 
# Python program to see Record Count 
# Per Partition in a pySpark DataFrame 
  
# Import the SparkSession and spark_session_id library 
from pyspark.sql import SparkSession 
from pyspark.sql.functions import spark_partition_id 
  
# Create a spark session using getOrCreate() function 
spark_session = SparkSession.builder.getOrCreate() 
  
# Read the CSV file 
data_frame = csv_file = spark_session.read.csv( 
    '/content/student_data.csv', sep=',', inferSchema=True, header=True) 
  
# Get number of partitions in data frame using getNumPartitions function 
print(data_frame.rdd.getNumPartitions()) 
  
# Get record count per partition using spark_partition_id function 
data_frame.withColumn("partitionId", spark_partition_id() 
                      ).groupBy("partitionId").count().show()
```
