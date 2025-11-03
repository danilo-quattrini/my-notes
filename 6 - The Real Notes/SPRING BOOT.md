2025-09-06 10:36

Status: #baby 

Tags: [[3 - Tags/Java]], [[Programming]], [[Back-End]]

---
# Structure your code
---
The best practice is to place your main Spring Boot Application in the root of your directory, above the other classes. The annotation we use in the main class is the `@SpringBootApplication` where it is acting as a package searcher

# Spring Boot Application
---
The class where we start our application is `SpringbootTutorialApplication`, and we run our app here for the first time, the structure of the class is like this:
```java
import org.springframework.boot.SpringApplication;  
import org.springframework.boot.autoconfigure.SpringBootApplication;  
  
@SpringBootApplication  
public class SpringbootTutorialApplication {  
  
    public static void main(String[] args) {  
        SpringApplication.run(SpringbootTutorialApplication.class, args);  
    }  
  
}
```

First of all we have the [[Programming Knowledge#Java annotations|annotation]] `@SpringBootApplication` that's the **entry point** of  the application that's activate three sub-annotations:
- `@EnableAutoConfiguration`
- `@ComponentScan`: where we find inside of it the annotation `@Controller` that finds the package where the application is located.
- `@SpringBootConfiguration`: where we import new configuration of the classes, that's an alternative of the standard Spring's annotation `@Configuration`.
Inside the main method we have the starting point of our application that is the method `SpringApplication.run(...)`, with inside the name of the main class and the args attribute
```java
//... packages
@SpringBootApplication
public class MyApplication {

	public static void main(String[] args) {
		SpringApplication.run(MyApplication.class, args);
	}

}
```
# Spring Boot Controllers
---
We use the [[Programming Knowledge#Java annotations|annotation]] `@RestController` that's a combined annotation of `@Controller` and `@RequestBody`,  to express that we are assigned that class as a Controller that handle the web requests like GET, POST, etc.

Besides we are saying that all the method that are inside the class with these annotations, they should return as values that are going to be in the  HTTP body.

Let's see in more detail the annotations `@Controller` and `@ResponseBody`:
- `@Controller`: says that the class is going to handle all the web requests GET, POST and more.
- `@ResponseBody`: ensures that return values are serialized into JSON or plain text directly in the HTTP response.
  
>[!info] **How does it works?**
>So every method that we are going to declare with `@GetMapping`, they send a string or  a JSON object into a HTTP request.

The `@GetMapping` annotation is used to map the GET request and map them to the `greeting()` method as this example below show.
```java
//...
@RestController  
public class GreetingController {  
    private static final String template = "Hello, %s!";  
    // This library it's necessary to handle unique ID's  
    private final AtomicLong counter = new AtomicLong();  
  
    @GetMapping("/greeting")  
    public Greetings greeting(@RequestParam(defaultValue = "World") String name){  
        return new Greetings(counter.incrementAndGet(), String.format(template, name));  
    }  
}
```


---
# Reference

[Mapping Request](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller/ann-requestmapping.html)
[HTTP REQ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods)