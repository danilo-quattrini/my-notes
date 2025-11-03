2025-09-25 10:13

Status:

Tags:[[Programming]], [[3 - Tags/Java|Java]], [[School]]

---

# Java
---
## Java annotations
---
https://www.geeksforgeeks.org/java/annotations-in-java/
## Java method signature
---
In Java programming, a method signature ==refers to the unique identifier of a method==. It ==consists of the method name and its parameter list==. The signature helps differentiate one method from another and allows the Java compiler to match method calls with their corresponding definitions. The method signature includes the following components:
![[MethodSignature.png]]
Java modifiers
---
Modifiers are keywords that you attach to classes, methods, or variables to change their attributes or behavior, these keywords serve as instructions to the Java compiler and runtime, indicating how to treat the elements they modify.

Modifiers in Java can be broadly categorized into two groups: 
- [[#Access modifiers|Access Modifiers]]
- [[#Non-access modifiers|Non-Access Modifiers]]

Each group serves a distinct purpose and applies to different programming scenarios.
### Access modifiers
Access modifiers help achieve this by setting visibility rules for classes, methods, and variables,Java provides four levels of access control through its access modifiers:
- `public`
- `private`
- `default`
- `protected`
#### `public`
The `public` modifier offers the highest level of visibility. ==Classes, methods, or variables declared as public can be accessed from any other class in the Java application==, regardless of the package they belong to.

>[!info]- **Where we use them?**
Using the `public` modifier is most common for utility methods and constants that need to be accessible from across the application.
#### `protected`
The `protected` It allows ==access to the protected class, method, or variable from within its own package (like default access) and also from subclasses even if they are in different packages==. 

>[!info]- **Where we use them?**
>This level of access is particularly useful when you want to hide certain details from general use but still allow access to those details in child classes.
#### `default`(no modifier)
When no access modifier is specified, Java uses default access, which is package-private. ==This means the class, method, or variable is accessible only within classes of the same package.==

#### `private`
The `private`all the classes, methods, or variables declared private can be accessed only within the class they are declared. Private access is the cornerstone of encapsulation, allowing you to hide the internal implementation details of your class from the outside world.
### Non-access modifiers
Non-access modifiers in Java don't control the access level of classes, methods, or variables but instead provide other functionalities. These modifiers include:
- `static`
- `final`
- `abstract`
- `synchronized` 
- `volatile`
These ones allows you to modify the behavior of classes,methods, and variables

#### `static`
The `static` modifier denotes that a particular field or method belongs to the class, rather than instances of the class. ==This means that the static member can be accessed without creating an instance of the class.==
```java
public class StaticExample {  
    public static int counter = 0; // Static variable  
      
    public static void incrementCounter() { // Static method  
        counter++;  
    }  
      
    public static void main(String[] args) {  
        StaticExample.incrementCounter();  
        System.out.println("Counter value: " + StaticExample.counter);  
    }  
}
```

>[!warning] **Watch out!**
>We didn't create an instance of the class who is declared `static`.
#### `final`
The `final` modifier ==indicates that the value of a variable cannot change, a method cannot be overridden, or a class cannot be subclassed==. Final variables must be initialized when they are declared or within the constructor of the class. 


>[!info]- **Where we use it?**
>Using final with classes and methods makes sure that they remain secure and unchanged throughout the execution of your program.
>

## Overriding vs Overloading
---
In Java, method _overloading_ and method _overriding_ both refer to creating different methods that share the same name. 
### Overloading (sovraccaricato)
Overloading a method, in simple terms, ==means creating a different method with the same name in the same class, but with a different parameter list.==
#### Example
For example, let's say you want to create a method that performs an addition of two numbers. This calculation is designed to return a number as its output. If your method handles parameters of type `int`, attempting to call it by passing values of type `double` as arguments results in a compilation error. 

For this reason, you might want to overload the method by creating a new version of that method that is able to handle a different type of input :
```java
public class Calculator {
    public int sum(int a, int b) {
        return a + b;
    }

    public double sum(double a, double b) {
        return a + b;
   }
}
```

### Overriding (sovrascritto)
The concept of ==overriding refers to redefining a method in a subclass that already exists in the superclass.==
When you call an overridden method using an object of the subclass type, Java uses the method's implementation in the subclass rather than the one in the superclass.
==Any subclass can generally override any method from a superclass, unless a method is marked with the `final` or `static` keywords.== The overriding method must not change the name and parameter list of the overridden method. 

>[!quote] Tips
it is good practice to use the `@Override` annotation when overriding a method: this annotation will check that the method is being overridden correctly, and will warn you if that's not the case. 

#### Example
In the following example, you'll see a class `Car` that extends the class `Vehicle`. The `Car` class overrides the `move()` method from the superclass, and this is made explicit by the use of the `@Override` annotation. The two methods are implemented differently in the method body.
```java
class Vehicle {
    public void move() {
        System.out.println("The vehicle is moving");
    }
}

class Car extends Vehicle {
    @Override
    public void move() {
        System.out.println("The car is moving");
    }
}
```

## Abstract class 
--- 
Java abstract class ==is a class that can not be instantiated by itself, it needs to be subclassed by another class to use its properties==. An abstract class is declared using the “abstract” keyword in its class definition.

Let's see an example there:
```java
// Abstract class abstract 
abstract class Sunstar {     
abstract void printInfo(); 
}  

// Abstraction performed using extends and overriding the method 
class Employee extends Sunstar {
	@Override 
	void printInfo(){         
		String name = "avinash";         
		int age = 21;         
		float salary = 222.2F;          
		System.out.println(name);         
		System.out.println(age);         
		System.out.println(salary);     
	} 
}   
```
In this example u see that we declare an abstract class and implemented like an interface into another class (in this case its own subclass).

For see the difference between Interface and Abstract class see this link [Abstract vs Interface](https://www.geeksforgeeks.org/difference-between-abstract-class-and-interface-in-java/)
## Interface
---
An interface is and abstract object that define a set of rule that an object/class in this case with Java, must follow when we *implement it*, we can find inside the interface static constants and abstract behaviors.

**Key Properties of Interface:***
- In java implement an interface is useful when we want to achieve [[Design Pattern#3.1 Abstraction|abstraction]].
- Variables inside the interface are by default [[#`public`|public]], [[#`final`|final]] and [[#`static`|static]].
- interfaces primarily define methods that other classes must implement, this can cause a break into the principle of [[SOLID Principals#I - nterface Segregation|Interface segregation]] if we don't split the role of an interface into multiples one.
Here we find an example on how the interface has been *implemented* inside the class `TestClass`.

```java
// Interface Declared
interface testInterface {
  
    // public, static and final
    final int a = 10;

    // public and abstract
    void display();
}

// Class implementing interface
class TestClass implements testInterface {
  
    // Implementing the capabilities of Interface
    public void display(){ 
      System.out.println("Geek"); 
    }
}
```

>[!info]- **How we use the interface?**
>Easy just use the keyword `implements` + `interface_name1, interface_name2, ...` inside the class we want to implement the method.
### Interface new features (From JDK 8+)
We use the `default` keyword before a method inside the interface, when we want to implement a *default* behavior, for all the classes we are going to *implements* the interface.

**Key concept**:
- Interfaces can define methods with default implementations.
- Useful for adding new methods to interfaces without breaking existing implementations.
```java
// interfaces can have methods from JDK 1.8 onwards
interface TestInterface
{
    final int a = 10;
    
  	default void display() {
        System.out.println("hello");
    }
}

// A class that implements the interface.
class TestClass implements TestInterface
{
    // Driver Code
  	public static void main (String[] args) {
        TestClass t = new TestClass();
        t.display();
    }
}
```


# Reference
---

 - [Java modifier](https://medium.com/@AlexanderObregon/beginners-guide-to-java-modifiers-d86a6b9d5dd9)
 - [Overriding vs Overloading](https://www.freecodecamp.org/news/method-overloading-and-overriding-in-java/) by _Mikael Lassa_
 - [Abstract Class](https://www.geeksforgeeks.org/abstract-classes-in-java/) by _GeeksForGeeks_



