---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - "[[Programming]]"
  - "[[Front-end]]"
author: Danilo Quattrini
---
# JavaScript
---
## The Event Loop



## The Core JS concept to grasp
---
### Data manipulation (Arrays & Objects)

Array methods like `.map()`, `.filter()`, and `.reduce()`. Object **destructuring** and the spread operator (`...`)

>[!info] Mini-Project Idea:
>Create a mock list of video games or movies (an array of objects). Write functions to filter them by genre, search for a specific title, and create a new list of just the titles.

### Methods of primitives
>[!error] REMEMBER
>Primitives **are not OBJECTS** in JavaScript, they create a "object wrapper" in the moment 
>we need a special functionality, but it's NOT AN OBJECT.
>```js
>	let str = "Hello!"
>	str.toUpperCase() // <-- they create the special Object called "wrapper" then after this line, the str it's not an object anymore.
>	 
>```

Primitives are the following ones: `string`, `number`, `bigint`, `boolean`, `symbol`, `null` and `undefined`

`null` and `undefined` they are defined as "the most primitives ones" because they don't have any "object wrapper", means they don't provide any methods like `string`, `numbers` and so on.
### Scope & Closures

**What to master:** The difference between `let/const` (block scope) and `var` (function scope). Understand how an inner function can "remember" variables from its outer function even after the outer function has finished running.

>[!info] Mini-Project Idea:
>Write a function called `createCounter()` that returns another function. Every time you call the returned function, it increments and logs a private count variable that can't be accessed from the outside

### Asynchronous JS Promises & Async/Await
**What to master:** 
- `fetch()`
- Promises
- `async/await` syntax.

>[!info] Mini-Project Idea:
>Use the free Pokemon API or Weather API. Write a script that fetches data for a specific item and logs a clean, formatted sentence about it to the console

### DOM Manipulation & Event Mastery
**What to master:**
- ``document.querySelector()`` ✅
- ``addEventListener()`` ✅
- dynamically creating HTML elements with JS. ✅
-  **Event Bubbling & Capturing:** Understand the order events fire.
- **Event Delegation:** Instead of adding a listener to 100 buttons, add one to the parent container. (Crucial for performance).
- **`IntersectionObserver`:** The modern way to handle "scroll into view" animations (better than `scroll` events).
- **`requestAnimationFrame`:** For smooth animations and game loops.
- **Shadow DOM:** Understanding scoped styles in web components

>[!info] Possible Interview Question
>When on an interview, a frontend developer gets a question about **“what’s a closure?”,** a valid answer would be a definition of the closure and an explanation that all functions in JavaScript are closures, and maybe a few more words about technical details: the `[[Environment]]` property and how Lexical Environments work.

### Map & Set
See more about **Map & Set**, how use  them in which context in real life it has a logical use.
[Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
[Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
# Reference
---
Array - [click here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
Scope & Closure - [click here](https://javascript.info/closure)
Asynchronous - [click here](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Async_JS)
Alghoritm complexity -  [click here](https://www.geeksforgeeks.org/dsa/complete-guide-on-complexity-analysis/) 

