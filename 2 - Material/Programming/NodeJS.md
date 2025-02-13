2024-10-02 21:01

Status: #devoleped 

Tag: [[Web Programming]] 
## How execute code in Node JS
The first way we are going to do is REPL
```js
$ node 

Welcome to Node.js v20.17.0.
Type ".help" for more information.

> type the js code that you want to execute
```

```js
node 'nome del file'.js
```
In this case we are execute a code that is inside a file and not directly on the terminal
**REPL and CLI**

First one mean Read Evaluate Printable, the second one mean Executable.
In the REPL one you're going to execute your code on the terminal. For going inside the REPL mode, just execute _node_ on your terminal , then whatever, you're going to write is going to be execute in the moment.

**How execute .js code on node?**
Execute your .js code on node just write _node_ in the terminal plus the name of the _file.js_

**GLOBAL variables**
In NodeJS there is no window because we cannot find any browser in NodeJS, so if we want to access to a specific part of the app we should use this global variable that mean that can be also used in any case if also the code is really complex.

***Tips** *****
- Arrow up for restart the previous command and avoid to rewrite it again.
- You can also avoid to write .JS at the end of the file, while execute the code.

## What is a promises
A Promise is a JavaScript object that represents the eventual outcome of an asynchronous operation every promise have 3 type of outcome:

1. ***pending***: means that the operation started, but it didn't ended so it's still processing, the result is undefined and the expression is waiting for a result.

2. __fulfilled__: means that the promise finished and return a value.

3. __rejected__: means that the promise didn't completed and the result is an error object. 

How we create our first _Promise_ first we need to say that you need to call a promise with and execute function for example:

```js
//We are going to define our function to pass throught the promise method
const executeFunction = (resolve, reject) => {
	//do something there
};
//I'm assigne to the variable the promise function
const ourVariable = new Promise(executeFunction);
```

This promise is going to take as a parameter a function called in this example `excuteFunction` that's going to run automatically when the constructor is called, The executor function in this case our `executeFunction` has two function parameters, usually referred to as the `resolve()` and `reject()`, these one are different function that the programmer didn't define but is the JavaScript that passed them:

- `resolve` is a function with one argument. Under the hood, if invoked, `resolve()` will change the promise’s status from `pending` to `fulfilled`, and the promise’s resolved value will be set to the argument passed into `resolve()`.
  
- `reject` is a function that takes a reason or error as an argument. Under the hood, if invoked, `reject()` will change the promise’s status from `pending` to `rejected`, and the promise’s rejection reason will be set to the argument passed into `reject()`.

Let's get in touch with the skeleton of the Promise function.
```js
const executeFunction(resolve, reject) => {
	if(someCondition)
	//if the condition is true then
	resolve('Condition resolved');
	else
	//if the condition is not resolved then do the other thing
	reject('I reject our condition');
};

//Call the Promise function

conts ourVariable = new Promise(executeFunction);
```

Now we are going to see our exercises that we did.
```js
const inventory = {

sunglasses: 0,

pants: 1088,

bags: 1344,

};

const myExecutor = (resolve, reject) => {

if (inventory.sunglasses > 0) resolve('Sunglasses order processed.');

else reject('That item is sold out.');

};

const myVariable = new Promise(myExecutor);

const orderSunglasses = () =>{

return new Promise(myExecutor);

};

const orderPromise = orderSunglasses();

  

console.log(orderPromise);
```
## How modules work?

In NodeJS all files are module, repeat, _all files are **modules**_ so in this case if we want to simplify the code and divide them, for their action , we can do that!!
```js
const John = 'John';
const Peter = 'Peter';
const SecretStuff = 'My secret stuff';

here is where you are going to export a module from a .js file 
in this case we are saying that we don't want that the constant SecretStuff 
will be export.

**module.exports = {John , Peter}**

```

For using them now we are going to use the global variable 'request' that we have seen before.
```js

const names = require('./fileName.js')

console.log(names);
/**
> node nomefile.js
{ jhon: 'Jhon', peter: 'Peter' }
**/
```
We are see that now in the variable they have saved the names John and Peter
```js
const names = require('./fileName.js')

console.log(names.John);
console.log(names.Peter);

/**
> node nomefile.js
	Jhon
	Peter
**/
```
### Alternative way to create modules and export them
We have two ways to export modules, they are at the end the same stuff but it's better to know them if we want to use one day.
```js

// 1° Way to do that is inline

module.exports.itemsList = ['item1' , 'item2'];

// 2° Way is to define into a variable

const person = {
	name: 'Bob'
}

module.exports.PersonList = person
```
## How install a new module

For install a new module in node you need to write this and the name of the module we want to install.
```js
npm install 'module name'
```
so for example if we want to install a module for using the file system, we are going to execute the command.
```
npm install fs

added 1 package, and audited 66 packages in 544ms

13 packages are looking for funding
  run `npm fund` for details

2 moderate severity vulnerabilities

Some issues need review, and may require choosing
a different dependency.

Run `npm audit` for details.
```
In this case the fs module is necessary for handle file that are located in your system, for example the function fs.readFile().

## Main Package 
--- 
- [[NodeJS#body-parser|body-parser]]
- dotenv
- express
- http
- mysql2
- [[Mongo DB|mongodb]]
---
### body-parser
`body-parser` is a library of Node.js, that allow to read the body of a HTTP request or also called request-body, when a client send data to the server, all these datas are inside the body of the HTTP request, Node.js is not capable to read data so `body-parser` is going to [[Programming Knowledge#^85c706|parse]] them.
#### When use the body-parser?
- for HTML modules from the POST
- from AJAX calls with JSON format
- for reading the body-request and read them easily
#### Example of his use
This is a html code example, a simple form that get informations, note of the POST method.
```html
<form action="/submit-form" method="POST">
  <input type="email" name="email" />
  <input type="password" name="password" />
  <button type="submit">Submit</button>
</form>
```
Here we are going to see how we are going to use the `body-parser`.
```js
const express = require('express');
const bodyParser = require('body-parser');

const app = express();

// Middleware di body-parser per leggere il body della richiesta in formato JSON o URL-encoded
app.use(bodyParser.urlencoded({ extended: true })); // per dati di form (x-www-form-urlencoded)
app.use(bodyParser.json()); // per dati in formato JSON

app.post('/submit-form', (req, res) => {
  const { email, password } = req.body;
  console.log(`Email: ${email}, Password: ${password}`);
  res.send('Dati ricevuti e processati!');
});

app.listen(3000, () => {
  console.log('Server in ascolto su http://localhost:3000');
});
```

1. We are going to require the module of `body-parser`, using the require and save into a variable, in that case `const bodyParser`.

2. we are going to use the `bodyParser.urlencoded({extend: true})` for encode the datas that we are going to retrive from the HTTP request, let's see each of the part of the code what they do.
   
	-  The `urlencoded` is begin used for read the datas from the HTML modules sent with `application/x-www-form-urlencoded`.

	- If the `extended:` is true is gonna read alla the datas in the correct way.