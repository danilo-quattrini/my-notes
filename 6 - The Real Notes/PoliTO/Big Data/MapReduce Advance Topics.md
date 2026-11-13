---
created: 2026-10-16
tags:
  - baby
topics:
  - BigData
  - Data
author: Danilo Quattrini
---
# MapReduce Advance Topics
---
## Configure Multiple Input Drivers
We use the `addInputPath` method in order to define different source of dataset where we can retrive the data to perform our calculation. 

This method is part of the class `MultipleInputs` (I think is a static method as I can call it directly without an instance of the class)
```java
MultipleInputs.addInputPath(job, new Path(args[1]),
TextInputFormat.class, Mapper1.class);

MultipleInputs.addInputPath(job, new Path(args[2]),
TextInputFormat.class, Mapper2.class);
```
The method addInputPath as four arguments:
1. The job we dedicate the it
2. A `Path()` that define where we take our data, with the `args[1]`  (argument of the command line where we define the place of the path) 
3. The Hadoop Type `TextInputFormat` we define of the input we gave to the input file. 
4. The last argument is the `Mapper.class` class we give the data that are contained into the path

In this way we can manage different different input format, but they must return the same format as the input data that we gave to the input path. The output of the mapper phase must be the same of the input date given.

## Distributed Cache
Some application need to share a library, archives or content of a small file. Is used the send a copy of the small to all the server into the cluster. The advantage of using a shared approach is that each node of the cluster to access the file doesn't need to interrogate the HDFS to get the content of the data, but the data is saved locally.

Below there's an example of the HDFS that share the file to all the nodes inside the cluster
![[Screenshot 2026-10-16 at 18.22.42.png]]
In the image we have the copies of the file into all the nodes above.

## Use the Distributed Cache
First we need to specify the file that we want to share with all the nodes in the cluster, that's done in the `Driver` class where we define a job method called:
```java
job.addCacheFile(path)
```

After when we run the program with Hadoop, Hadoop will generate a copy of the file in every mapper or reducer class that use the file. The file will be read locally from the Mapper and Reducer class inside the `setup` method. 

>[!info] Improvement
>With this approach we are going to avoid from the Mapper class and the Reducer class to read the file directly from the Hadoop Distributed File System that could slow the 