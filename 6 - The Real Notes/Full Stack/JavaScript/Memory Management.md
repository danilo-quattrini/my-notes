---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - "[[Programming]]"
  - JS
  - "[[Front-end]]"
author: Danilo Quattrini
---
# Memory Management
---
Memory management it's the concept where the JS engine come in play and handle the memory of JS under the hood. Any variable, function and object reference are allocated in a section in memory, that we will see how it works.

## Memory Life cycle
Memory life cycle has 3 phase:
1. [[#Memory allocation|Allocation]]
2. [[#Memory Usage| Usage]]
3. [[#Memory Deallocation| Deallocation]]
### Memory allocation
**It happens when you create a variable, object, or function** in [JavaScript](https://www.geeksforgeeks.org/javascript/javascript-tutorial/), the engine allocates memory to store the value. This can happen in several ways:

- ****Primitives:**** Simple data types like [numbers](https://www.geeksforgeeks.org/javascript/javascript-numbers/), [strings](https://www.geeksforgeeks.org/javascript/javascript-strings/), and [booleans](https://www.geeksforgeeks.org/javascript/javascript-boolean/) are stored directly in memory. They are typically allocated on the [stack](https://www.geeksforgeeks.org/javascript/implementation-stack-javascript/).
- ****Objects and Arrays:**** These are more complex data structures. The reference to the data is stored in memory, and the actual data is often stored on the [heap](https://www.geeksforgeeks.org/javascript/min-heap-in-javascript/).

### Memory Usage
**Once memory is allocated, the JavaScript engine uses it as the program runs**. When you reference variables, objects, or functions, the engine accesses the memory where the data is stored.

### Memory Deallocation
**When a variable, object, or function is no longer in use, the memory allocated to it should be freed.** The JavaScript engine automatically determines when memory is no longer needed and deallocates it.

## Garbage Collection
This concept it's explained in more detail in the note [[Garbage Collection]] but shortly it the alghoritm js handle variable and objects that are not been used anymore by the program.

## Types of Memory in JS

# Reference
---
[Geek For Geeks](https://www.geeksforgeeks.org/javascript/memory-management-in-javascript/)
