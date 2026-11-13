---
created: 2026-09-25
tags:
  - baby
topics:
  - BigData
  - Data
author: Danilo Quattrini
share_link: https://share.note.sx/2aqp0xci#wavDAbcDr2+xq7ic8lXTrToxq2TzCMqQWEksTqzZboY
share_updated: 2026-09-27T16:01:13+02:00
---
## Meaning of Big Data
---
>[!quote] Definition
>We define **big data** as the big amount of data that are around the world.

We can define **data analytics** as the approach to take data from a source like a CSV, Relational Database or other sort of data generator, analyze them with tools and extract value from these data.

**Nowcasting**: we are trying to explain now, how many people are affected to flu, to do that we use big data algorithms on them.

>[!question]
>Which are the data we can use to solve this task? 
>

This is the main question we need to ask, to ourself if we want to make prediction and then later work with algorithms. 

>[!question]
>How can I use the data to resolve a problem? 

That's also important to know because there are also solution of problems with already well known data, already collected from someone else.

## Data Input
The amount of data that we have on internet it's really big and we need to save them into a datacenter. These data are generated 4 different sources one from Users with media contents like Facebook posts, Instagram, X-Twitter and other from health and scientific computers, IoT and Log files.

## The 5'V
- The **volume** refers to the vast amount of data generated. Big data is distinguished by their size, which can be much larger than traditional data. The management and analysis of large volumes of data require appropriate infrastructure and tools. 
	  
- Velocity  indicates the speed at which data is generated and collected. In the context of Big data, data can be generated in real time or in high frequency. The ability to process and analyze data in real-time therefore becomes crucial. The goal is to obtain useful information and responsiveness in business decisions. 
  
-  The **variance** concerns the diversity of data types present in the context of Big data. Data can come from different sources, such as social media, sensors, mobile devices, corporate databases, and can be: structured, unstructured or semi-structured. The management and analysis of this variety of data requires flexible and adaptable solutions.
  
- **Veracity** concerns the quality and reliability of data. In the context of Big data, it is important to ensure that the data collected is accurate, complete and error-free. It is necessary to implement quality control processes to ensure that the data is reliable and that the information obtained is valid. 
  
- Finally, the **Value** represents the potential value that can be drawn from the data. Big data offers the opportunity to analyze and leverage data to obtain valuable information, identify trends, patterns and correlations, improve decision-making, identify new business opportunities and offer a personalized customer experience.

## Failures 
If a failures happens the system will catch it automatically, so no worries on this field. There are different source of failure, like hardware, software electrical, unavailable of resource due to overload

## Networks Bandwidth
>[!warning] Exam question
>How many data we will send on the networks? That's a question that could be in the exam, because if we are not aware of how many data we send on the network it would be bad as fuck.

the bottleneck if big amounts of data need to be exchanged between nodes/servers, like moving 10Tb of data would be complicate if we need to send data from one server to another.
	 
>[!danger]
> **Data should be moved across nodes only when it is indispensable**

## Solution
The solution to transfer a lot of data through the network layer it's to divide data into different distributed disks, where each one hold a **portion of code**. Because data are big, but code it's small so we send code to the server, it's called **Data Locality**.

It's easier to process parallely different data portion instead of 1 large dataset. So the concept it's to separate big data partition into different blocks, where each block it's stored into a server, with part of the data.![[Screenshot 2026-09-27 at 10.51.27.png]]
These server calculate and elaborate data in order to return a result, where each result of this server it's combined into a final result![[Screenshot 2026-09-27 at 11.08.54.png]]
The blue arrows shows that each server after they compute the result, they will combine all the results into one big output. With this approach we cannot solve all the problem of the big data era, for instance, we cannot comunicate through each server during the processing part, but the communication of each server it's handle at the end when they calculate the finale result.
## Node
A node it's a computer that holds data and process them in order to return an output. For instance a node could be a **Server**, that's compose as different part as it follows.
![[Screenshot 2026-09-27 at 10.53.28.png]]

Where the CPU and the Memory (RAM) handle the small data part, that means all the **small data** we are going to upload it's in the main memory. Where the Disk that could be an HDD or a SSD handle the large part of the data. Which means the data will be divided in different small chunks. These chunks of data will be analyzed by the memory and the result saved in the Disk, that's called **Data Mining**.![[Screenshot 2026-09-27 at 10.56.38.png]]

### Cluster of Nodes
When we talk about cluster of nodes we are define the group of server that are interlinked to each other through a Gigabit Ethernet connection, in order to handle enormous amount of data. These cluster are useful because they can handle the work of analyze and process the data through each other, that means all data are stored and save into every cluster and shared in order to perform a computation.![[Screenshot 2026-09-27 at 10.59.56.png]]
Each one they have speed hard disk and good connection in order to send data to one server into another.
#### Scale Up vs Scale Out
There are two different approach to scale up a server:
1. **Scale Up** (Vertically): means that we are going to change our old component to new one, adding for instance new CPU or more main memory, you cannot scale linearly with the amount of data.
2. **Scale Out** (Horizontally): It's used in NoSQL databases, it's simplier because we just buy a new server to improve the amount of the time to analyze the data, t hat's because they are adding more nodes ([^1]commodity servers).
If you need to analyze a big amount of data the **Horizontal Scalability**, it's the best approach, because you need to use high performance computer, but it's important to analyze how many data we can analyze in 1 seconds.

The challenge that we need to chase it's what we are going to do if one node of the cluster it's going to fail? How we can resolve the problem? The solution it's through redundancy, which means copy the same piece of data in different nodes, that increase complexity but save the data in case one node it's going to fail.

## Big Data Problems
The problem we are going to chase in the big data field it's to iterate hover a big amount of record/objects, like scanning each record of a database. Then extract important information from these records, aggregate intermedian results and the output the global result. **From each input element you should extract something small**
# Reference
---

[^1]: The word **commodity** here simply expresses that they are built from freely available parts and based on open standards
