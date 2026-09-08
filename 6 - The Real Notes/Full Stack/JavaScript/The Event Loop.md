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
# The Event Loop
---
## JS Behavior 
JavaScript it's single threaded, means can perform one task at time, for instance let's see at this code example:
![[Screenshot 2026-07-01 at 16.07.34 1.png]]

JavaScript Engine execute code line-by-line, means that it will go in each line of the script and each line will be add to the stack as [[Execution Context|Execution Context]], so javascript can take a lot of time if there's a time consuming operation. 

## Time consuming operation
This time consuming operation it's called **blocking function**, in this example wee see that there's a time consuming operation that JS should handle before going further:
```js
function timeConsumingOperation(){
	let counter = 0;
	for(let i = 0; i < 1e9; i++){
		counter++;
	}
	console.log(counter)
}

function importantTask() {
	console.log(`Important Task`);
}

timeConsumingOperation()
importantTask()
```
In this example the **Call Stack** has in its execution context the `timeConsumingOperation` that's still running before the `importantTask`, that because of the synchronous manner of JS.

## WEB API
For solve this problem JS has some asynchronous Web API that permits to our program to perform other task in the meanwhile of an outgoing **blocking function**, these Web API are the following:
![[Screenshot 2026-07-01 at 18.27.37.png]]

These Web API have different feature that allow to off-load the **Call Stack**, these are the **callbacks** (function that are inside another function) and **Promises** (an outgoing object that will be resolve or reject).

## Example of Web API
Let's start with the **callbacks** functions, when there's an operation like an event listener from a button:
```js
button = document.getElementById(`#random-button`)

button.addEventListener("click", () => {console.log(`Hello!`)})
```

We don't know from the user when the button will be clicked, but in the meanwhile the **[Call Stack](https://www.geeksforgeeks.org/javascript/what-is-the-call-stack-in-javascript/)** its performing its operation, means processing other functions execution, the callback function inside the `addEventListenere` it's stopped in the [WEB API](https://developer.mozilla.org/en-US/docs/Web/API) until this operation it's perform.

When the operation of clicking the button it's been perform, the function it's not inserted in the **Call Stack** but it will be add in the **Task Queue** (Macro Queue)
![[Screenshot 2026-07-01 at 18.39.38.png]]

In the **Task Queue** there are all the callback function we defined but we didn't perform because they where still waiting to their execution, when they are executed they will be place in the queue and here it's when the **EVENT LOOP** come in place.

## What's doing the Event Loop?

>[!warning]
>The role of the **Event Loop** it's to check if the **Call Stack** it's empty, if it's so, then it will take the first task from the **Task Queue** and move from the stack, following the **FIFO** order (First In First Out)

Below we see the Event Loop taking the first task from the queue and place it to the Call Stack.
![[Screenshot 2026-07-01 at 18.46.09.png]]

As we can see there's either another queue that's called **Microtask Queue**.

## What's the Microtask Queue
The Microtask queue it's the one who will be use by:

**Promise handler**:
![[Screenshot 2026-07-01 at 19.01.46.png]]

**Async body functions after the execution of the await**:
```js
async function asyncFunc() {
	await...
	// After the await this is add in the microtask
}
```

Then it will ad to the Microtask Queue the `queueMicrotask(() => {})` function and the `new MutationObserver(() => {})`

The Microtask queue **have the priority** after the Macrotask queue (task queue), the Event loop when it has checked the call back stack and see that there is no operation to perform, it will first check the **Microtask Queue**:
![[Screenshot 2026-07-01 at 19.05.13.png]]
# Reference
---
[Web API](https://developer.mozilla.org/en-US/docs/Web/API)