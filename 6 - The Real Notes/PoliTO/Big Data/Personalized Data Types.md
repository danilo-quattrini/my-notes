---
created: 2026-10-09
tags:
  - baby
topics:
author: Danilo Quattrini
---
# Personalized Data Types
---
We can Personalized Data Types that are useful when the value of a key-value pairs is a complex data type, we should use the interface:
```
org.apache.hadoop.io.Writable
```
and use the methods
```java
public void readFields
public void write()
```

To do this we need to define a new class, we call it for instance:
```java
public class SumAndCountWritable implements 
org.apache.hadoop.io.Writable {
	private int sum = 0;
	private int count = 0;
	
	@Override
	public void write(DataOutput out) throws IOException {
		out.writeFloat(sum);
		out.writeInt(count);
	}
	
	@Override
	public void readFields(DataInput in) throws IOException {
		sum = in.readFloat();
		count = in.readInt();
	}
	
	public String toString() {
		String formattedString = new String("sum="+sum+"count="+count);
		return formattedString;
	}
	
	//------- GETTER AND SETTERS OF sum AND count -----
}
```
The order of the variables we define inside the function `write` must be the same as the `readFields`, THIS WILL NO THROWS ERRORS BUT IT WILL RETURN BAD RESULTS. So avoid to do this:
```java
	@Override
	public void write(DataOutput out) throws IOException {
		out.writeInt(count); // !!! THIS IS THE LINE THAT CAUSE THE ERROR
		out.writeFloat(sum);
	}
	
	@Override
	public void readFields(DataInput in) throws IOException {
		sum = in.readFloat();
		count = in.readInt();
	}
```

Personalized Data Types can be used also to manage complex keys, to do that we need to implement the interface:
```java
org.apache.hadoop.io.WritableComparable
```
and use the functions, on for the key comparison/sort:
```java
compareTo()
```
and split them in groups:
```java
hashCode()
```
# Reference
---

	