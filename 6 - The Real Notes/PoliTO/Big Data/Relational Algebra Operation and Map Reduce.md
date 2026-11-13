---
created: 2026-10-22
tags:
  - baby
topics:
  - BigData
  - Data
author: Danilo Quattrini
---
![[Screenshot 2026-10-22 at 08.58.19.png]]# Relational Algebra Operation and Map Reduce
---
Implement SQL queries with map reduce, there are different operations like selection, projection, join, aggregation and so on. With map-reduce we can use these operations. 

We use these operation into a map-reduce environment because we want pre-process our data, before going to be analyzed into different algorithms, **we should avoid duplicates record**.

The data are stored are saved into a file inside the HDFS.

## SELECTION
The filtering pattern is useful to apply a condition into a set of record that we want to filter values into a table with a condition. 

Each output of the query is a (key, value) pair 

## PROJECTION
For each record of a table we want to keep only the attribute in the columns 
![[Screenshot 2026-10-22 at 08.54.11.png]]

It's equivalent in SQL to:
```sql
SELECT DISTINCT PSurname
FROM Professors
```

To do that we should return always a key value pairs, where we place in the mapper as key the values of the column and the value is **null**
![[Screenshot 2026-10-22 at 08.55.07.png]]

## UNION
Given two input files, associated as two table, the union operation is performed only if the **two files has the same schema**, and the record of each file shouldn't be null.
![[Screenshot 2026-10-22 at 08.58.29.png]]

To implement it we need data from import two file and we use the **MultipleInputData**, the output of the Mapper class should return the same type of the input ![[Screenshot 2026-10-22 at 09.00.13.png]]

In the Reducer the key value is the content of the record from both of the files, that's **called one time for each distinct record**

## Intersection
We just return only the value that are in the both of the file, so the value that's the same in both files
![[Screenshot 2026-10-22 at 09.04.01.png]]
The key is the value of the table, where the value is the name of the table.

The reducer is called one time for each table, where the output of the reducer is only emmited only if the value of table 1 is either in table 2, like the intersection operation.
![[Screenshot 2026-10-22 at 09.04.45.png]]

If you count the number of values into the iterable of the reducer and it's bigger or equal to 2 it means that there's an intersection.

## Difference
$$R-S$$
I want save the records that are in the table $R$ but not in the table $S$, this operation is applied in record level
![[Screenshot 2026-10-22 at 09.08.03.png]]

## JOIN
to see in design patter of the [[MapReduce Patterns]] part

## AGGREGATION & GROUP BY