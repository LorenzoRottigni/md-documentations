# 26 - Spark

Spark is an open source project on Apache and it's one of the most popular libraries of python for big data.


Spark is avaiable in both local and cluster mode.


For cluster mode is meant a distributed environment, where the data is stored in a cluster of machines.


In a local mode the data is stored in the local machine, in distributed mode data is stored between multiple nodes and nodes are orchestrated by a master node providing more processing power and memory.


Distributed systems also provide fault tolerance, if a node fails the data is still available in other nodes.


Spark can use data stored in a variety of formats, including Cassandra, AWS S3, HDFS, CSV, JSON, Parquet, and more.

## Spark architecture

At the core of Spark is the idea of a Resilient Distributed Dataset (RDD), a collection of data that is split into chunks and spread across multiple nodes.


- RRDs are immutable, once created they cannot be changed.
- RRDs are lazily evaluated, the data inside an RDD is not processed until an action is called.
- RRDs are fault tolerant, if a node fails the data is still available in other nodes.
- RDDs are cached in memory, this makes them faster to access than data stored on disk.
- There are 2 types of RDDs operations: transformations and actions.
- Transformations are lazy operations, they are not executed until an action is called.
- Actions are operations that return a result to the driver program or write it to storage.
- RDDs expose some methods to perform actions and transformations: map, filter, reduce, collect, count, take, saveAsTextFile, and more.
## Distributed architecture - Hadoop

In simple words Handoop is a software framework that makes possible to store and process big data in a distributed environment.
It uses a distributed file system called HDFS (Hadoop Distributed File System) and a processing framework called MapReduce.
- HDFS duplicates the data across multiple nodes to ensure fault tolerance.
- HDFS uses chunks of data called blocks, the default size of a block is 128MB.
- each block is replicated 3 times by default, so if a node fails the data is still available in other nodes.
- smaller blocks provide more parallelization during processing

Spark ecosystem includes:
- Spark SQL: a module for working with structured data.
- Spark Streaming: a module for processing real-time streaming data.
- MLlib: a library of machine learning algorithms.
- GraphX: a library for manipulating graphs and performing graph-parallel computations.


### MapReduce
MapRaduce is a programming model for processing big data in a distributed environment.

It is composed by two steps:
- Map: the input data is divided into chunks and processed in parallel by multiple nodes.
- Reduce: the output of the map step is processed in parallel by multiple nodes.

It consists in a Job Tracker and multiple Task Trackers.
The Job Tracker sends code to run on the Task Trackers.
Task Trackers allocate CPU and memory for the tasks and monitor the tasks on the worker nodes.