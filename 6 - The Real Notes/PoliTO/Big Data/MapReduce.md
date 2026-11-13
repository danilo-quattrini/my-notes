---
created: 2026-10-02
tags:
  - baby
topics:
  - BigData
author: Danilo Quattrini
---
# MapReduce
---
## Questions
- What's MapReduce?
- How it works MapReduce?
- What's the function `map` doing in MapReduce?
- What's the function `reduce` doing in MapReduce?
### Map
- How it works the `Mapper` class in Java?
- Why we don't use the Java Type like `String`, `int` and we use instead `Text`, `IntWritable`
### Reduce
## MapReduce and Functional Programming
You just have two function  `map` and `reduce`, it's good because there are just only two functions bur for complex application it's different The programming model appears quite limited and strict local list
### Map
It is applied over each element of an input data set and emits a set of `<key, value>` pairs, it can be viewed transformation over each element of a data set, where each input of data is executed for each data in input, so the function is called for each input.

>[!warning] N.B
>**The Map class  instances run on every different machines** (the worker nodes), potentially dozens of them, each in their own separate JVM process. Hadoop literally serializes your job configuration and ships it over the network to each worker, which then deserializes it and constructs a fresh `Mapper` object locally.
>
>So any `static` variable we define into a `Mapper` class it will not work because the static variable will not be read into any different mapper.
### Reduce
It's used to each `<key,value>`  with the same key and emits a set of (key, value) pairs and final set result. Reduce phase can be viewed as an **aggregate operation** this aggregation function is a function **r** defined by developers,  **r** is invoked one time for each distinct key and aggregates all the values associated with it

### Map & Reduce in action
![[Screenshot 2026-10-02 at 16.22.57.png]]

It's possible to parallelize the map and reduce phase. The map is always parallelizeble wherase the reduce phase it's not paralellazable
![[Screenshot 2026-10-02 at 16.26.41.png]]

### Map in Java
In Java the Map is a class that extends `Mapper` class with where Maps are the individual tasks which transform input records into an intermediate records. The **transformed intermediate records** need not be of  the same type as the **input records**. 

A given input pair may map to zero or many output pairs.

There are three important variable to understand from the `Mapper` extended class:
```java
class MapperBigData extends Mapper<LongWritable, Text, Text, IntWritable>
```

| Position | Type           | Meaning                                                           |
| -------- | -------------- | ----------------------------------------------------------------- |
| 1        | `LongWritable` | **Input key**: the position (byte offset) of the line in the file |
| 2        | `Text`         | **Input value**: the content of the line                          |
| 3        | `Text`         | **Output key**: the word                                          |
| 4        | `IntWritable`  | **Output value**: the number 1                                    |

**Why `Text` and `IntWritable` instead of `String` and `int`?** Data in Hadoop travels over the network and is saved to disk, so it must be easy to convert to bytes. Hadoop has its own “wrapper” types for this, called **Writable** types. `Text` is the Hadoop `String`, `IntWritable` is the Hadoop `int`, and `LongWritable` is the Hadoop `long`.

Who give the input to the mapper class?
- `TextInputFormat` (set in the Driver) reads the file and hands the mapper **one line at a time** as `(offset, line)`. For example
```
(0,  "the cat sat on the mat")
(23, "the dog sat on the log")
```

Let's see the `map` method in the `MapperBigData` here:
```java
protected void map(  
        LongWritable key,   // Input key type  
        Text value,         // Input value type  
        Context context) throws IOException, InterruptedException {  
  
        // Split each sentence in words. Use whitespace(s) as delimiter   
       // (=a space, a tab, a line break, or a form feed)  
	    String[] words = value.toString().split("\\s+");  
          
        // Iterate over the set of words  
        for(String word : words) {  
            // Transform word case  
            String cleanedWord = word.toLowerCase();  
              
            // emit the pair (word, 1)  
            context.write(new Text(cleanedWord),  
                         new IntWritable(1));  
        }  
}
```
In this code we are take a `value` in input  and convert it into a string into a way that we can use the `split()` function to separate each phrase of the sentence into the file into different words and save them into an array of `String[]`

then we have this part of code
```java
for(String word : words) { 
	String cleanedWord = word.toLowerCase();
	context.write(new Text(cleanedWord), new IntWritable(1)); 
}
```
we read the arrays of strings and then make them lowercase in order to avoid camelcase scenario that will generate 

**I cannot parerilize the reduce phase**

### Reducer in Java
The reducer class is the one who is dealing with summing all the occurences of the word found in the file. 

This is the class
```java
class ReducerBigData extends Reducer<Text, IntWritable, Text, IntWritable>
```

always four input for the reducer class

| Position | Type          | Meaning                           |
| -------- | ------------- | --------------------------------- |
| 1        | `Text`        | **Input key**: the key            |
| 2        | `IntWritable` | **Input value**: number 1 of many |
| 3        | `Text`        | **Output key**: the word          |
| 4        | `IntWritable` | **Output value**: the total count |

>[!warning]
>**Important rule:** the reducer’s input types (1 and 2) must **match the mapper’s output types** (3 and 4). The mapper’s output is the reducer’s input.


The `reduce` method is called **once per distinct word**, not once per occurrence:

```java
protected void reduce(Text key, Iterable<IntWritable> values, Context context)
```

- `key` = the word, e.g. `"the"`
- `values` = **all** the 1s emitted for that word by **all** mappers, e.g. `[1,1,1,1]`

```java
int occurrences = 0;
for (IntWritable value : values) {
    occurrences = occurrences + value.get();
}
context.write(key, new IntWritable(occurrences));
```

Start at 0, add up every value, then emit `("the", 4)`. `value.get()` converts an `IntWritable` back to a normal Java `int`, in this case we are working with an iterable.

>[!warning] REMEMBER
>An Iterable in Java is iterate only once it's not possible to iterate over it twice.
# Reference
---

