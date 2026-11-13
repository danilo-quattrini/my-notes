---
created: 2026-10-15
tags:
  - baby
topics:
  - BigData
  - Data
author: Danilo Quattrini
---
# Exercises
---
>[!warning] Before doing anything
>You need to answer every question before write a MapReduce program
>- Input key/value: what do they represent?
>- Output key/value: what do they represent?
>- What does the Mapper do to go from one to the other?
>- Does the Reducer do real aggregation, or is it just pass-through?

## Select outliers
**Input:** a collection of (structured) textual files containing the daily value of PM10 for a set of
sensors
![[Screenshot 2026-10-15 at 09.20.27.png]]

**Output**: the records with a PM10 value below a user provided threshold (the threshold is an argument of the program)

The mapper method can return this two different types of key-value pairs for the values that are:
```
("s1,2016-01-01", 20.5) # 1° Solution

("", "s1,2016-01-01\t20.5") # 2° Solution

(NullWritable, "s1,2016-01-01\t20.5") # 3° Solution if we don't want to define groups
```

If we need to share these data we use the configuration object and access it through the context of the map method.

```java
Configuration conf = this.getConf() // configuration object 

// Then we can define a personalized property that must be a string
conf.set("maxThreshold", args[2])
```

>[!warning]
>All personalized properties must be before the creation of the `Job`, if you define a personalized property before 
>```java
>Job job = Job.getInstance(conf)
>```


In the mapper class we can retrive the value of the argument through the `setup` method discussed [[Combiner#In-Mapper Combiner|here]] 

```java
threshold = Float.parseFloat(context.getConfiguration().get("maxThreshold"))
```

## Exercise 21
![[Screenshot 2026-10-22 at 09.41.50.png]]
We use only the MAPPER CLASS because we don't aggregate nothing, so we do this to only use the mapper class:
```java
job.setNumReduceTasks(0);
```
In order to only use the Mapper class

We use **distributed cache** in order to mantain the value that are in the stopword file, in all instances of the mapper class.![[Screenshot 2026-10-22 at 09.43.56.png]]
The part where `job.addCacheFile(new Path("filename.txt").toUri())`, in order to save the file. 

### Grouping and return coumulative total
![[Screenshot 2026-10-23 at 16.14.42.png]]

Io farei un mapper che dia la data e il mese semplicemente senza il giorno, con value il valore del guadagno mensile.
```
("2015-11", 1000)
("2015-11", 1305)
("2015-12", 500)
("2015-12", 750)
("2016-01", 345)
("2016-01", 1145)
("2016-02", 200)
("2016-02", 500)
```

Poi nella fase di reduce farei semplicemente, questo è per il primo job, mentre il secondo.

```java
// example "2015-11", [1000, 1305]
for(IntWritable value: values) {
	count += value.get()
}
context.write(key, new IntWritable(count))
```
![[Screenshot 2026-10-23 at 16.29.12.png]]

You use the summarization pattern (to see this one too), then we have a second job that's dedicate to calculate the average, who will get as input the output of the previous job (the one we sum the value for each job).

So the couple of the mapper output would be:
```
("2015", 2305)
("2015", 1250)
("2016", 1490)
("2016", 700)
```

The code would be this one.
![[Screenshot 2026-10-23 at 16.30.02.png]]


## Social Network Exercise

Text file with a pair that identify:
```
user1,user2
```
user1 is a friend of a user2 and we should only output only one line that identify all friend of a specific user we want to write into a command line.

I will need only the map class where I just filter the user that is inserted in input and only get the user who is friends to, for instance

I'm interested in just the user who is friends with so the mapper would be.

```java
String[] values = values.toString().split(",")

for(String value: values) {
	if(value.equals(inputSomething)) {
		context.write(NullWritable.get, value)
	}
}
```

In the reducer then you would just inline the result, that's the useful thing to do in the reducer
```java
String listOfFriends = "";
for(Text value: values) {
	listOfFriends += value.toString()
}
context.write(NullWritable.get, new Text(listOfFriends))
```
