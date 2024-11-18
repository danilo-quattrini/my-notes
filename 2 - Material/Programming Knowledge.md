2024-10-04 13:25

Status: #baby 

Tags: [[Programming]]

---
# Programming Knowledge

## Name of all the characters in english 

I'm struggling to remember all the name in english of all the characters but now, I will remember all of them with this table.

| **Symbol** | **Name**             |
| ---------- | -------------------- |
| ~          | Tilde                |
| `          | Grave Accent         |
| !          | Exclamation Mark     |
| @          | At sign              |
| #          | Hash                 |
| ˆ          | Caret                |
| :          | Colon                |
| ;          | Semi Colon           |
| \|         | Vertical Pipe        |
| /          | Slash                |
| \          | Back Slash           |
| >          | Greater Than         |
| <          | Less Than            |
| .          | Period or Dot        |
| {          | Open Brace           |
| }          | Close Brace          |
| [          | Open Square Bracket  |
| ]          | Close Square Bracket |
| ,          | Comma                |
| &          | Ampersand or And     |

## Method signature

In Java programming, a method signature ==refers to the unique identifier of a method==. It ==consists of the method name and its parameter list==. The signature helps differentiate one method from another and allows the Java compiler to match method calls with their corresponding definitions. The method signature includes the following components:

![[MethodSignature.png]]
## Java modifiers
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
The `public` modifier offers the highest level of visibility. ==Classes, methods, or variables declared as public can be accessed from any other class in the Java application==, regardless of the package they belong to. Using the public modifier is most common for utility methods and constants that need to be accessible from across the application.
#### `protected`
The `protected` It allows ==access to the protected class, method, or variable from within its own package (like default access) and also from subclasses even if they are in different packages==. This level of access is particularly useful when you want to hide certain details from general use but still allow access to those details in child classes.
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
We didn't create an instance of the class who is declared `static`.
#### `final`
The `final` modifier ==indicates that the value of a variable cannot change, a method cannot be overridden, or a class cannot be subclassed==. Final variables must be initialized when they are declared or within the constructor of the class. Using final with classes and methods makes sure that they remain secure and unchanged throughout the execution of your program.

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

// Abstraction performed using extends 
class Employee extends Sunstar {
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
In this example u see that we declare an abstract class and implemented like an interface into another class (in this case its own subclass). **

For see the difference between Interface and Abstract class see this link [Abstract vs Interface](https://www.geeksforgeeks.org/difference-between-abstract-class-and-interface-in-java/)
## What is an API

API stand for **A**pplication **P**rogramming **I**nterface and can mean a lot of different things but a _web API_ is a collection of predefined ways of, or rules for, interacting with a web application’s data, often through an HTTP request-response cycle.

![[ExampleWEBAPI.png]]
In this case the web API is reading data from the website db and it can also delete, update and create new field.

### Authorization and Authentication

_Authentication_ is the process of validating the identity of a user. One technique for authentication is to use logins with usernames and passwords.
Web applications can also use external resources for authentication. You’ve likely logged into a website or application using your Facebook, Google, or Github credentials; that’s also an authentication process.

_Authorization_ controls which users have access to which resources and actions. Certain application views, like the page to edit a social media personal profile, are only accessible to that user. Other activities, like deleting a post, are often similarly restricted.

## MEAN or MERN
Why we use that? 
Because in this case we are going to say that the mix of front-end and back-end is call, _stack_, that's mean a mix of front and back resources. 
**MEAN** ([MongoDB](https://en.wikipedia.org/wiki/MongoDB "MongoDB"), [Express.js](https://en.wikipedia.org/wiki/Express.js "Express.js"), [AngularJS](https://en.wikipedia.org/wiki/AngularJS "AngularJS") (or [Angular](https://en.wikipedia.org/wiki/Angular_(application_platform) "Angular (application platform)")), and [Node.js](https://en.wikipedia.org/wiki/Node.js "Node.js")) is a [source-available](https://en.wikipedia.org/wiki/Source-available "Source-available") [JavaScript](https://en.wikipedia.org/wiki/JavaScript "JavaScript") [software stack](https://en.wikipedia.org/wiki/Software_stack "Software stack") for building dynamic web sites and web applications A variation known as MERN replaces Angular with [React.js](https://en.wikipedia.org/wiki/React_(JavaScript_library) "React (JavaScript library)") front-end

![[Pasted image 20241030185408.png]]
## Arrow Expressions

 Arrow expressions has allowed developers to ==omit parts of the function they don’t need==. This means that it allows your code to become more maintainable and organized.

When using an arrow expression, we do not use the `function` declaration. To define an arrow expression you simply use: `() => { }`. You can pass arguments to an arrow expression between the parenthesis (`()`).
```js
// Defining an anonymous arrow expression that simply logs a string to the console.  
console.log(() => console.log('Shhh, Im anonymous'));  
  
// Defining a named function by creating an arrow expression and saving it to a const variable helloWorld.  
const helloWorld = (name) => {  
  console.log(`Welcome ${name} to Codecademy, this is an arrow expression.`)  
};  
  
// Calling the helloWorld() function.  
helloWorld('Codey'); //Output: Welcome Codey to Codecademy, this is an Arrow Function Expression.
```
# Reference
---
 - [Java modifier](https://medium.com/@AlexanderObregon/beginners-guide-to-java-modifiers-d86a6b9d5dd9)
 - [Overriding vs Overloading](https://www.freecodecamp.org/news/method-overloading-and-overriding-in-java/) by _Mikael Lassa_
 - [Abstract Class](https://www.geeksforgeeks.org/abstract-classes-in-java/) by _GeeksForGeeks_