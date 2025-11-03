2025-10-03 09:43

Status: #devoleped 

Tags: [[Programming]], [[3 - Tags/Java|Java]], [[OOP]]
# Java Records
---
We use classes to hold datas from databases, queries, person data, customer data and so on, in this way the data we save are immutable, that means **we cannot change them after we assign the value to each variable**.

In Java before the release 14, it was possible to do that thought all these steps:
- *private* field with the *final* modifier
- *getter* method to retrive the information of these fields
- *public constructor* to assign the data 
- *equals* method that returns *true* for object of the same class and when all fields match,.
- *hashCode*: this method return the same value if all the fields match.

Let's see an example below of how many lines of code we have there:
```java
public class Person {

    private final String name;
    private final String address;

    public Person(String name, String address) {
        this.name = name;
        this.address = address;
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, address);
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        } else if (!(obj instanceof Person)) {
            return false;
        } else {
            Person other = (Person) obj;
            return Objects.equals(name, other.name)
              && Objects.equals(address, other.address);
        }
    }

    @Override
    public String toString() {
        return "Person [name=" + name + ", address=" + address + "]";
    }
```

There are too many lines of code, where **we have a lot of boilerplate code** and we obscure the purpose of our class, **to represent the person data**.

The purpose of this class is just to represent datas, we should just sho the **name** and the **address**, A better approach would be to explicitly declare that our class is a data class.

## Solution
---
The solution after Java 14 it's use the class as a **Record**, where we just declare the class name and the type of variable we want to use.

>[!info] **Note:**
>Records in Java are immutable, that means we can't change the data inside of it after we assign a value
```java
public record User(String name, String email, String password)
```
# Reference
---
[Java Record Keyword](https://www.baeldung.com/java-record-keyword)
