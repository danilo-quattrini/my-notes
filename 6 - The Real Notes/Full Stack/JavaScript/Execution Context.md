---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - "[[Front-end]]"
  - "[[Programming]]"
  - JS
author: Danilo Quattrini
---
# Execution Context
---
Code from the source it's not interpreted as it is when we write it, but there's a **Parser**, that translate our JS code into a machine understandable code. This operation is perform by many different browser engine, for instance we have V8 from Google, SpiderMonkey from FireFox and Chakra from IE. 

They have all the common operation to take a source code in JS and parse it to a machine understandable code, that the computer can work with.

## How JS Execute the Code?
Every engine we defined before has it's own **Execution Context**, but what's this context i cite? 

>[!important] Execution Context
>It's a dedicated space that each engine use to parse and execute a JS code.

The Execution Context contains the code that's currently running, and everything that aids in its execution.

During the Execution Context run-time, the specific code gets parsed by a parser, the variables and functions are stored in memory, executable byte-code gets generated, and the code gets executed.

There are two types of **Execution Context**:
- **Global Execution Context** (GEC): it's the default and can only be one, this context is **where all the code that's outside to a function will be executed**
- **Function Execution Context** (FEC): It's related to the context where it will be executed inside a function, these are within the **Global Execution Context** and **they will be create at every function call**

## How they are created?
There are two phase during the creation of an **Execution Context** (GEC or FEC):

1. Creation phase.
   
2. Execution phase

###  Creation phase
This phase contains three stage that will be perform in both execution context, but with different behavior.
1. Creation of the Variable Object (VO)
2. Creation of the Scope Chain
3. Setting the value of the `this` keyword
# Reference
---
[freeCodeCamp](https://www.freecodecamp.org/news/execution-context-how-javascript-works-behind-the-scenes/)
