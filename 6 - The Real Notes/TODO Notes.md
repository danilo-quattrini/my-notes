---
created: 2026-03-14T10:48:00
tags:
  - baby
topics:
author: Danilo Quattrini
share_link: https://share.note.sx/twgf691x#Pp3EieYG5wM6/4uZOkVrOi3jf1unqZQpATaOz3GpNO0
share_updated: 2026-03-30T11:59:54+02:00
---
# Nextsuite

Todo list for NextSuite project, divided in **features**, **fixes**, **refactor** and **things to start**.
### Features
#### **COMPLETED**
- Add a reference to the generated summary that says the system it's using AI inside of it (COMPLETE) ✅.
- Show the field suggestion to the report page of the customer.  (COMPLETE) ✅
#### **WORKING ON** 🛠️
- Implement **send email to invite people inside the company**. (COMPLETE) ✅
- SHIFTING THE MAILING SYSTEM TO THE NOTIFICATION ONE, that's a better version of mailing, because **you can send notification to different channel** and make the app, multipurpose. (URGE) ✅
- Create the company concept with the employee inside of it. ✅
#### **TO REVIEW**
- Introduce the Model Employee for the company, with skill, attribute and the same things as the the customer (that's the authenticated user the employee, I should only add the skill, attribute and review model).
- Introduce all the permissions with roles, inside the same Company ( **Laravel Policy** CustomerPolicy class to implement), this should be done after the employee are inside the company and the concept of notification with, invitation link has been concluded.
- Introduce an homepage view.
### Fix
- Fix update customer issue that doesn't display the error on the image. (COMPLETE) ✅
- Find a way to fix the toast notification inside the app, where the `$this->dispatch()` method should work everywhere.
- Company should be complete with all data, and be able to add employee, concept of grouping models into another model.
### Refactor
- Company creation page to change the layout.
- Company details view, to change the layout.
- User profile section to review and create page to. 

### To Start
- Document generation from customer skill, attribute , reviews and anagraphics.
- Introduce Service concept, which type of service, the app should contains?
- Complete profile security, with 2AUTH and more operations, like UPDATE and DELETE.

# Personal Finance Project

## Account ✅
- Add an IBAN value to the account and test if it's valid or not. ✅
- Add **account types** — savings accounts earn interest monthly, checking accounts have transaction limits
## Transaction operation
All the operation that are involved the account, for instance deposit an amount of money in the balance or withdraw the found you want.
- Add a `transfer(targetAccount, amount)` method that moves money between two accounts. ✅
- Add **categories** to transactions — groceries, rent, salary — and generate a summary by each of them.
## History operation ✅
An history of operation it's an array that track all the transaction made into an account, for example if the user make a deposit, this transaction will be saved in its personal account history.
- Add a `getHistoryByType('deposit')` that filters transactions by type. ✅
- Add a `getLastTransaction()` that returns the most recent operation.  ✅
- Add an **audit log** with timestamp and make it impossible to modify. ✅
## Monthly report 🛠️
Group transactions by month and calculate total deposits, total withdrawals, and net balance change for each month

## Budget system 🛠️
Set a spending limit per month, throw a warning when the user is close to the limit

## Bank object 🛠️
That holds multiple accounts — it should be able to **find accounts**, **calculate total assets across all accounts**, and **generate a full bank report**
## Notification system 🛠️
When balance drops below a threshold, trigger a callback function that the user provides when creating the account.

# TODO  1 week
- Complete DOM manipulation topic on JS and make some exercises on it, like the mini-project with the TODO-list (HTML-CSS-JS).  ✅
- Understand the concept of `this` changes context (global, object method, arrow function) and how it affects in each cases and understand where this it's an object or a global. ✅
- **`call`, `apply`, `bind`:** How to manually control the `this` context.  ✅
- **Prototypes & Inheritance**: Understand how `class` extends `class` under the hood (`__proto__`), do other exercises on this concept. ✅
- **Proxy & Reflect**: Advanced object interception (useful for state management later) ✅.
- **`Map` & `Set`:** You know arrays, but `Map` is better for key-value pairs where keys can be objects ✅
- **Destructuring & Spread:** Deep dive into object destructuring and the `...` operator. ✅
## FINAL PROJECT ✅
**Goal:** Build a system that manages product inventory, enforces business rules, and provides a dynamic UI.

- **Fix** that stock it's undefined in the item object. ✅
- **Fix** UI where the description it's not wrap on its container. ✅
- **Feat** Implement a button to **sell** and **add** item in the inventory. ✅

# TODO Week 2
- Iterator 🛠️
- WeakMap & WeakSet [click here](https://javascript.info/weakmap-weakset)
- `localStorage` & `sessionStorage`: Persisting data in the browser.
- `Cookies`, document.cookie how they works and why use them?
-  `IndexedDB`: For storing large amounts of data (like a mini-database in the browser).
-  **JSONP vs. CORS:** Understand why some APIs block requests and how to handle them.
- **Debouncing & Throttling:** Optimizing event listeners (e.g., search input shouldn't trigger 50 API calls per second).

# Concept to see in JS
## DOM & Event Mastery
- **Event Bubbling & Capturing**: Understand the order events fire. ✅
- **Event Delegation**: Instead of adding a listener to 100 buttons, add one to the parent container. (Crucial for performance). ✅
-  `IntersectionObserver`: The modern way to handle "scroll into view" animations (better than `scroll` events). ✅
-  `requestAnimationFrame`: For smooth animations and game loops.
-  **Shadow DOM**: Understanding scoped styles in web components. ✅

## Data & Storage
- `localStorage` & `sessionStorage`: Persisting data in the browser.
-  `IndexedDB`:** For storing large amounts of data (like a mini-database in the browser).
-  **JSONP vs. CORS:** Understand why some APIs block requests and how to handle them.
- **Debouncing & Throttling:** Optimizing event listeners (e.g., search input shouldn't trigger 50 API calls per second).

##  Modules & Tooling

- **ES Modules (`import` / `export`):** Understand the difference between CommonJS and ES Modules.
- **NPM / Yarn:** How to manage dependencies.
- **Bundlers (Webpack / Vite):** How JS files are combined and optimized for production.
- **Transpilation:** Why we use Babel (converting modern JS to older browser versions).
## Performance & Security

- **XSS (Cross-Site Scripting):** How to sanitize user input before putting it into `innerHTML`.
- **Memory Leaks:** How to stop listeners from hanging on and crashing the browser.
- **Web Workers:** Running heavy JS calculations in a separate thread so the UI doesn't freeze.
## Testing 
- **Unit Testing:** Using Jest or Vitest to test your logic functions.
- **DOM Testing:** Using tools like Cypress or Playwright to test the UI behavior.