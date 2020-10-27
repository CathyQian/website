## What is Hadoop?
Hadoop is an open-source software framework for **storing data** and **running applications on clusters** of commodity hardware. It provides massive storage for any kind of data, enormous processing power (via MapReduce) and the ability to handle virtually limitless concurrent tasks or jobs.

Relational Database Management System or RDBMS is a database management system designed specifically for relational databases which refers to a database that stores data in a structured format, using rows and columns. It is the basis for SQL, and for all modern database systems like MS SQL server, IBM DB2 and MySQL. RDBMS offers consistency of transactions, availability, but **lacks scalability**.

Hadoop is dealing with non-relational database, which overcomes the limits of RDBMS (lack of scalability). It can handle much more data than RDBMS or NoSQL database. However, it's **not a replacement of RDBMS but rather a supplement**.

A Hadoop setup contains 
- open-source data storage: HDFS
- Processing API: MapReduce (for document indexing)
- Other projects/libraries: HBase, Hive, Pig etc 

You can **create a Hadoop cluster** in open souce platform such as Apache Hadoop, or commercial distributions such as Cloudera, or public cloud such as AWS-EC2 instance or GCP-GCS instances.

Hadoop supports the following three file system:
- HDFS (Hadoop Distributed File System)
- Regular file system
- Cloud file system (i.e., AWS: S3, Azure: BLOB) (which becomes more popular as the IT industry is moving to Cloud)

## Common Hadoop libraries

**HBase** is an open-source **non-relational distributed database** modeled after Google's Bigtable and written in Java. It is developed as part of Apache Software Foundation's Apache Hadoop project and runs on top of HDFS or Alluxio, providing Bigtable-like capabilities for Hadoop.

**Apache Hive** is a **data warehouse** software project built on top of Apache Hadoop for providing data query and analysis. Hive gives an **SQL-like interface** to query data stored in various databases and file systems that integrate with Hadoop. 

**Apache Pig** is a high-level **platform for creating programs** that run on Apache Hadoop. The language for this platform is called Pig Latin. Pig can execute its Hadoop jobs in MapReduce, Apache Tez, or Apache Spark.

**Spark** is a fast and general engine for **large-scale data processing** which is gaining quite a lot of momentum in the data science and machine learning community.

## MapReduce
MapReduce is initially created by Google to index information on the internet. It serves as the processing API for the Hadoop ecosystem.

**MapReduce is a processing technique and a program model for distributed computing**. The MapReduce algorithm contains two important tasks -- Map and Reduce. Map takes a set of data and converts it into another set of data, where individual elements are broken down into tuples (key/value pairs). Secondly, reduce task, which takes the output from a map as an input and combines those data tuples into a smaller set of tuples. As the sequence of the name MapReduce implies, the reduce task is always performed after the map job.

The major advantage of MapReduce is that it is **easy to scale data processing over multiple computing nodes**. Under the MapReduce model, the data processing primitives are called mappers and reducers. Decomposing a data processing application into mappers and reducers is sometimes nontrivial. But, once we write an application in the MapReduce form, scaling the application to run over hundreds, thousands, or even tens of thousands of machines in a cluster is merely a configuration change. This simple scalability is what has attracted many programmers to use the MapReduce model.

## Compare with Spark
Hadoop can be easily mixed up with Spark given that both words appear frequently together.

Apache Spark is a fast and general engine for **large-scale data processing** (not for data storage) that **can use Hadoop as cluster resource manager** (i.e., Qubole implementation of Spark; there are other options as well). It consists of a Spark core and a set of libraries similar to those available for Hadoop. 

Apache Spark does not come with in-built cluster resource manager and distributed storage system.

- You can choose Apache YARN or Mesos or **Hadoop**(popular and that's why Hadoop and Spark are easily mixed up) as cluster resource manager for Apache Spark.
- You can choose Hadoop Distributed File System (Yes Hadoop), Google Cloud Storage, AWS S3 as storage system.

Apache Spark has the following advantages:

- **Speed**: Apache Spark achieves high performance for both batch and streaming data, using a state-of-the-art DAG scheduler, a query optimizer, and a physical execution engine. It runs much faster than previous approaches to work with Big Data like classical MapReduce, as it runs on memory (RAM) which makes the processing much faster than on disk drives.

- **Ease of Use**: Write applications quickly in Java, Scala, Python, R, and SQL. Spark offers over 80 high-level operators that make it easy to build parallel apps. And you can use it interactively from the Scala, Python, R, and SQL shells.

- **Generality**: Combine SQL, streaming, and complex analytics.Spark powers a stack of libraries including SQL and DataFrames, MLlib for machine learning, GraphX, and Spark Streaming. You can combine these libraries seamlessly in the same application.

- **Runs everywhere**: Spark runs on Hadoop, Apache Mesos, Kubernetes, standalone, or in the cloud. It processes data in HDFS, HBase, Hive, or any input format. 

## Apache Spark vs Hadoop MapReduce

- Apache Spark is 10~100 times faster than Hadoop MapReduce. This is mainly because Spark processes data in memory while MapReduce process data in local disk.
- Apache Spark supports streaming, machine learning, complex analytics etc, while MapReduce comprises simple Map and Reduce tasks.
- Apache Spark is suitable for real-time streaming while MapReduce is suitable for batch processing.
- Apache Spark requires more lines of code than MapReduce.

## Cascading (Extra)
Cascading is a software abstraction layer for Apache Hadoop and Apache Flink. Cascading is used to create and execute complex data processing workflows on a Hadoop cluster using any JVM-based language, hiding the underlying complexity of MapReduce jobs.

## Summary

Hadoop is a software framework for **data storage** and **running applications** in clusters, while Spark is an engine for **large-scale data processing**. Spark does not have its own cluster resource manager and thus sometimes use Hadoop as cluster resource manager (i.e., in Qubole). MapReduce is the main Hadoop data processing API, however **Spark is much faster than MapReduce** and thus gaining more popularity, especially at the data science and machine learning field where large and complex data processing is needed.


References:

1. https://spark.apache.org/
2. https://www.linkedin.com/learning/learning-hadoop-2/getting-started-with-hadoop
3. https://cwiki.apache.org/confluence/display/Hive/Tutorial
4. https://www.tutorialspoint.com/hadoop/hadoop_mapreduce.htm
