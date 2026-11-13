---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - BigData
author: Danilo Quattrini
---
# Spark
---
Is an apache framework available in the apache eco-system, this is a big data framework to analyze data offline, but also **analyze stream of data**. These are characterized by:
- **Generality**: differente work-loads, operators, job sizes
- **Low latency**: sub-second.
- **Fault Tolerance**: there are always exceptions and error that are well handled.
- **Simplicity**: often come from generality.

## Spark History
![[Screenshot 2026-10-23 at 18.07.54.png]]

## Motivations
Why we need to use this big data framework?

1. **We cannot analyze stream of data**.
2. Iterative job with MapReduce involves a lot of disk I/O for each iteration.
![[Screenshot 2026-10-23 at 18.11.54.png]]

For this reason we need a different solution, and apache spark has this solutions.

## Spark Solution
**I need to use the main memory of the server to save intermediate results**, that's because the memory costs are more less than the disk
![[Screenshot 2026-10-23 at 18.14.38.png]]

We use the main memory to write the data into memory, we can split up the solution of the application from 10 to 100 times faster than the disk.

If we want to execute different queries into the local file system this will cost a lot of different jobs and it will costs a lot of time
![[Screenshot 2026-10-23 at 18.17.31.png]]

![[Screenshot 2026-10-23 at 18.18.10.png]]
## Spark RDD (Resilient Distributed Data sets) 
![[Screenshot 2026-10-23 at 18.19.06.png]]

**Transformation** is the process to transform data and then use the **Actions** methods to combine the transformations.
![[Screenshot 2026-10-23 at 18.20.41.png]]

## MapReduce vs Spark
![[Screenshot 2026-10-23 at 18.21.01.png]]

### Differences using Machine Learning Alghoritms
![[Screenshot 2026-10-23 at 18.25.20.png]]

## Spark Components
![[Screenshot 2026-10-23 at 18.26.21.png]]

We have several integrated component, **Spark Core** is in charge to schedule the jobs. Four components at the top, where we have **Spark SQL structured data**, used to perform query with SQL using SQLite, with different methods. 
**Spark Streaming real-time**, use to analyze stream in real time. Now the source of data are input stream, not a file into a File System.

**Machine Learning Library**, where we have some machine learning algorithms

**GraphX (Graph Processing)**: using to analyze nodes.

Then we have three schedulers
- Standalone Spark Scheduler
- YARN Scheduler same used by Hadoop
- **Mesos**

## Structure of Spark Program
There is the *driver* as the programs who runs on each functions defined by the user and **parallelized the operations into a cluster**, the main abstract data structure that apache spark is **Resilient (flessibile) distributed Data**
### Resilient Distributed Data sets (RDDs)
It's a data structure used in Spark that are collections of data separated into differente blocks
These are stored in the main memory of the executors running in the nodes of the cluster (when it is possible) or in the local disk of the nodes.

![[Screenshot 2026-10-23 at 18.38.10.png]]

Like we see in the image we have a collections of items from `item1` to `item12`, this collection of item is partitioned in three parts (from `item1` to `item4`, then `item5` to `item8` and so on), each partition is given to every cluster (server) where it can operate it on it.
### Create an RDD
To create an RDD we use a file into an HDFS that takes this file in the Driver program that take it and transform it.

>[!info] Persist RDD
>We can persist RDD in order to share the RDD in different parallel

>[!warning] How handle failures?
>To handle failures RDD's recover them from the node.
