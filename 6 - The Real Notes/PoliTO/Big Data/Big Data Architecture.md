---
created: 2026-09-25
tags:
  - baby
topics:
  - BigData
  - Data
  - "[[School]]"
author: Danilo Quattrini
share_link: https://share.note.sx/94in8oij#zxm39VrheEk20caVb/VghisdK4LERKaiUYe4ZzivwMc
share_updated: 2026-09-27T16:16:38+02:00
---
# What's a Big Data Architecture.
---
>[!quote]
>It's an information system to analyze big amount of data, from traditional database system

Sometimes we are going to analyze streams of data, sometimes big data solution involve one or more of the following types of workload:
- **Batch processing** means analyze big amount of data offline;
- **Real-time processing**: means analyze stream of data;
- **Interactive exploration** of big data;
- **Predictive Analytics** and **Machine Learning** alghoritms;

We should consider big data architecture when you need to **process data in volumes to large** for a traditional database, **transform unstructured data for analysis** and reporting also it's useful if we need to **analyze unbounded stream of data in real time** or **with low latency**. In case you don't reach one of this cases YOU DON'T NEED TO USE ANY OF THEM!!.

Select solution for the right task, you should use the right framework for the right task.
## Lambda Architecture
There are different solution nowadays that can handle data in different approach, but most of them have some issue related to **high latency** or they are not **human-fault tolerant**
>[!quote] Definition Hadoop #1 
>Hadoop to parallelize large-scale batch computation on very large amount of data, but each computation have a **really high latency**. Means you don't use *Hadoop* if you want to avoid low-latency results

>[!quote] Definition NoSQL #2
>With NoSQL approach you achieve the **scalability**, by offering you a limited data model. But sometimes reduce these data into these data model can be complex and also **databases are mutable**, so they are **not human friendly tolerant**. If something it's mutable you can introduce error too.

>[!quote]
>The Lambda Architecture it's an architecture to analyze big amount of data that provides access to batch-processing and stream processing methods with a hybrid approach. The lambda architecture it's a solution to solve problem of **computing arbitrary functions**

With this architecture it's possible to avoid hardware failures and humans errors. We should also be able to **balance latency**, **throughput** and **fault tolerance**.

The Lambda Architecture depends on data model that is **append-only**, that means it's not possible to update or change data, in this way you are not going to lose data. You **CAN ONLY ADD DATA**

### Queries
Everything in the lambda architecture it's base on queries, where you apply a function that you apply on data. Like this
$$queries = f(x)$$
Where we have the function $f$ that execute its operation into an input collection of data and take the result of this function. These function are characterized with some properties, like so:
- **Latency**: the time needed from the system to execute an operation and return a result.
- **Timeliness**: means if the data you return are consistency or fresh, that's mean if the data are recent or no.
- **Accuracy**: the result of the function it's accurate of the result we wanted, because sometimes we are searching for accuracy and other time we are searching for quick response time.

### Structure
![[Screenshot 2026-09-27 at 12.41.14.png]]
The workflow of the Lambda Architecture it's the following one:
1. All the time that we are receiving data from the outside these data are splitted in two paths, the **Batch Layer** and the **Speed Layer**.
2. In the **Batch Layer** the row data are saved into a master dataset, means we are using the **approach of append-only**, we discuss before to append new data into the **master dataset**. This dataset it's **IMMUTABLE** (cannot change or delete data inside of it) and **APPEND ONLY** (only new data can come inside the master dataset).
3. **Serving Layer**: It's the layer that deals with the request of the query made from the user outside, that means, the serving layer it's a middleware from the **outside user and the master dataset**, these queries are executed on the **batch views**
   >[!warning]
   >Note that the batch views we see from the image, they are always updated when a new record will be added into the master dataset.
   
   4. The **speed layer** it's dedicated part of the Lambda Architecture, where there are real time views that they are used to save values.
The user can use with the queries both layers, for instance if the data we need it's saved in the real-time views, then we are going to use these ones.

>[!example] Example
>Let's take in input a stream of tweets and historical tweets
>![[Screenshot 2026-09-27 at 15.40.58.png]]
>In the example shown from the professor the input that we are going to analyze are data that are saved into the historical dataset + the data read from the input stream. From the image we have the batch views, that are the numbers of time that the word Polito has been found in the master-dataset, that's 1000. In the speed layer, we have a new tweet read from the input stream: "This is Polito", the speed layer at begin it's 0, then it will turn 1 or more number in case we found other word of Polito into the input stream. At the end the result of the query it's the sum of the occurences found in the service layer + the speed layer, that's 1001.

**The lambda framework works well if the function (the query) we apply it's associative and commutative**
![[Screenshot 2026-09-27 at 15.49.27.png|427]]![[Screenshot 2026-09-27 at 15.49.45.png|433]]

The input of data we are going to send on these two layers it's made with Kafka, another framework to manage input streams.

For the Immutable master-data we use the [[Hadoop|Hadoop]] HDFS (Hadoop Distributed File System), it's very efficient for storing big amount of data, for the batch processing part to compute the result you want store we are gonna use [[Spark|Spark]] or [[Hadoop]],  the output of the analysis part (the pre-computed views) that generate views we can use Hadoop Hive. 

The speed layer we are gonna use [[Spark]], the framework to analyze stream of data. The result we are gonna save can be saved with Hadoop Hive or some Not Relational Databases.

# Reference
---

