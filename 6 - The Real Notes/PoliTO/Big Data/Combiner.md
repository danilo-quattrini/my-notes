---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Combiner
---
We use it to reduce the amount of data we send on the network, let's see an example **without combiner**. How we can reduce the amount of (key, value) pairs into the network? The solution is going to give the real number of occurences of the word
![[Screenshot 2026-10-09 at 16.34.08.png]]
We can reduce the pairs of each instances of mapper class, we send less data into the server.

**Combiner** is a class to reduce the pairs of (key, value) pairs, that analyze the pairs of a specific mapper. Where the combiner aggregate the result of the mapper class.
![[Screenshot 2026-10-09 at 16.35.45.png]]

Combiner is an instance of the abstract class of the Reducer (org.apache.hadoop.mapreduce.Reducer.class), it works fine if the function is **commutative** and **associative**. The system will not raise error but it will return wrong results. The system can decide if the combiner is useful of useless, we don't know if the system will execute the combiner or not, it's not decidable, so we cannot use conditions to shows the output of some result fi the combiner has been used or not.

The input give to the combiner that's the result of the mapper class the output of the combiner **must be the same of the mapper input type**.

In 99% of cases the combiner class is similar to the reducer class, let's take an example. 

Into the combiner we use a new job function called `setCombinerClass` into the `Driver` class
```java
job.setCombinerClass(WordCountCombiner.class)
```
but because the combiner class is the fucking same as the reduce, we can use the name of the reduce instead of the class, like this:
```java
job.setCombinerClass(ReducerBigData.class)
```
The combiner is frequently used for efficiently reason

## In-Mapper Combiner
It's better than the traditional combiner approach. The mapper class it mandatory to implement the `map` method, but it can also introduce another method called `setup`, that's called once for each instance of the mapper class. 

### `setup` method
The `setup` method is used to set the values of the in-mapper variables, is it similar to the behavior of the constructor in c++. 

There's another method called `cleanup`, **always called for each instance of the mapper class or the reducer class instances**, used to calculate statistics.

These methods return (key, value) pairs based on the in-mapper variables values.

### The solution
The basic idea is to initialized some local variable that are into the `setup` method and in the `cleanup` method we analyze the local statistics 
 ![[Screenshot 2026-10-15 at 09.00.56.png]]
 We initialize an associative array in the `setup` method where we save the occurences of the word that we are counting (instead of counting them into a variable we save the counting into an associative array). Then after we save the result into an associative array, in the `cleanup` method we iterate over the associative array and return the pairs.

The maximum number of occurences of the world that it could saved in the `A` associative array, in the worst case scenario they are all different words that are saved into the file
>[!warning] 
> The function should be associative and commutiative, if yes we can use the in-mapper combiner, and we need to be aware of the amount of data we need to save in the main memory. If there are too many data to save and it's over the size of the main memory. DON'T USE THE SOLUTION.
 
 # Reference
---

