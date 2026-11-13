---
created: 2026-09-25
tags:
  - baby
topics:
  - BigData
  - Data
author: Danilo Quattrini
share_link: https://share.note.sx/1a0tt3vf#aHbzKV9U++oGcVRrgYsSV5BQq0tccLJeW/H3y7BUbG0
share_updated: 2026-09-27T17:23:51+02:00
---
# Definition
---
>[!quote] Defintion
>Apache Hadoop is an open-source framework designed for the distributed processing of large volumes of data on computer clusters. It uses a simple programming model to allow scalable and efficient computing on large amounts of data, which can be structured or unstructured. Hadoop was created to solve problems related to the processing of Big Data, ensuring reliability, fault tolerance and scalability. Hadoop's architecture is based on four main components:
>- **Distributed Data Storage** (Distributed File System), that it's possible to store data in several server into a distributed approach.
>- **Distributed Data Processing** each server compute the data and the result it's send to the network
>- It's open source under Apache License
>- Borrow the concept Idea from the Google File System for Google 

it's design for intensive workloads and usually doesn't use the CPU for high demanding tasks wherease the HCP (High Performance Computing) it's a computer for high computing capacity that's measured with **floating-point operations per seconds** (FLOPS) and they are design for CPU high intensity tasks, it's usually used for "small" data sets.

## Hadoop VS HPC
There are different usage of Hadoop and different field where we can use (High Performance Computing). The **Hadoop Framework it's used for high intense workload**, without using the power of the CPU. The **High Performance Computing** it's used for analyze small partition of data that they need high performance computing, like floating point numbers or other hard task, in this scenario we use the CPU power. 
## Hadoop Main Components
Distributed Big Data Processing Infrastructure based on the MapReduce programming paradigm. It will **provide an high-level abstraction view** and  a **fault tolerant** mechanism that makes Hadoop reliable where if each node or task fails the they will be automatically handle by Hadoop.

Then there's **Hadoop Distributed File System** (HDFS) it's an high availability distributed storage that is able to manage faults, correctly.![[Screenshot 2026-09-25 at 18.41.09.png]]
It works like the image we see above, where we have different servers that each of them implement the HDFS. Each server has a disk to store file system data that are divided in different chunks.

## HDFS 
It's specifically design to store big amount of data and manage failures, in this distributed system you save files that have dimension of gigabytes. NO UPDATE OR DELETE OPERATION, these operation are probite in the Hadoop Distributed File System.

### Chunk Structure
Each input file it's split into different **chunks**, the chunks are the block with $C_{n}$ in the image where these chunks are distributed into several server. The block that it's going to be created (chunk) will be copied 3 times in each server, to ensure persistence and availability. 

The size of the chunk it's 64 to 128MB.

>[!example] Example of a file that's been save into the Hadoop File System
>Suppose we have a file that's big 129MB and a chunk / block can store only 128MB of data. How many blocks we need? The answer it's 2, the first block it's for the 128MB part and the 1MB to another block. ![[Screenshot 2026-09-27 at 17.02.56.png]]
>So the $C_{0}$ block it's dedicate for the 128MB part of the file and the $C_{1}$ for the 1MB part, in the image above the its creating 2 copy of the block $C_{0}$ and $C_{1}$, but usually into the HDFS there are 3 copies

Another example it's that if we have to upload another file into the HDFS, with a size of 24MB, then the space we left before in the example, from the chunk $C_{1}$ that's only 1MB that's occupied, these block CANNOT BE USED ANYMORE. 

So it will be create another block to save the File 2 with the size of 24MB without using the space of $C_{1}$![[Screenshot 2026-09-27 at 17.08.58.png]]

>[!info] N.B
>It's better to concatenate file and create a big file, instead of single files with few MB
### Master Node
Usually there's a Master Node that's a server used to save file system labels and metadata, like mapping between the name of a file and a location of its chunks and ofter there's a copy of this node to avoid single point of failure.

## Word Count Example
![[Screenshot 2026-10-02 at 16.09.38.png]]
Suppose that we have an input file of 100gb and number of distinct word occuring, where the wrong scenario one server it's going to analyze all the different work. We can use the scale approach in terms of data if Given twice the amount of data, the word count algorithm
takes approximately no more than twice as long to run.

>[!quote] In terms of resources
>Given twice the number of servers, the word count algorithm takes approximately no more than half as long to run, because each server process $\frac{1}{2}$ of x data and $\frac{1}{2}$   execution time to compute

# Reference
---

