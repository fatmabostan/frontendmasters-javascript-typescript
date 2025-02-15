<div align="center">

# 📚 JavaScript Notes

## Based on "JavaScript: The Hard Parts v2" by Will Sentance (FrontendMasters)

</div>

## 🌟 Section 2: JavaScript Principles 
- JavaScript executes code line by line-known as the `thread of execution` (take the code, do it.)
- `Saves data` like strings, arrays, and functions `in memory` so we can use it later.
- `Identifiers` don’t store values, they point to memory locations where values exist!
- When JavaScript first sees a function, it doesn’t execute it right away. Instead, it stores the function in memory and only runs it when called.
- When you define a function, JavaScript stores it in memory.
- When you call a function using (), JavaScript executes the function immediately—it doesn’t store the call itself.
- Memory can only store values, can't store "go do something"

| **Term**                 | **Meaning**                                     | **Example**      |
|-------------------------|---------------------------------|----------------|
| **Declaration**         | Creating a variable without assigning a value  | `let x;`         |
| **Initialization**      | Assigning a value to a variable for the first time | `let y = 5;`     |
| **Uninitialized Variable** | A declared variable that has not yet been assigned a value | `let z; // Uninitialized (value is undefined)` |
 
### What is hoisting?
- Hoisting in JavaScript means that variable and function declarations are moved to the top of their scope during the compilation phase, before the code executes.
- However, only function declarations and variable declarations (without initialization) are hoisted—not assignments.
```js
// Variables declared with var are hoisted but initialized as undefined.
console.log(x); // ❌ Undefined, but NO ERROR (declaration hoisted)
var x = 10;
console.log(x); //10

//Variables declared with let and const are hoisted, but not initialized (TDZ ERROR).
console.log(y); // ❌ ReferenceError: Cannot access 'y' before initialization
let y = 20;
console.log(y); //20
```

| **Term**                  | **Definition**                                                 |
|---------------------------|---------------------------------------------------------------|
| **Function Declaration**   | Stored in memory during the initial phase (hoisted).         |
| **Function Expression**    | Stored only when the code reaches it (not hoisted).          |
| **Hoisting**              | Declarations are hoisted, but expressions are not.           |

```js
// Function Declaration (Stored & Hoisted)
// Function declarations are hoisted, stored in memory first and can be used before their definition. 
greet(); // ✅ Works! Because it's hoisted

function greet() {
  console.log("Hello!");
}

// Function Expression (Not Hoisted)
// Function expressions are only stored when the code runs.
sayHello(); // ❌ ReferenceError: Cannot access 'sayHello' before initialization

const sayHello = function() {
  console.log("Hello!");
};
```
- `Execution Context` = `Thread of Execution` + `Memory`
- Every function is like a mini app so calling a function creates a new `Execution Context`
- Once the function finishes running, its Execution Context is removed from memory.

<div align="center">
    <img src="https://i.imgur.com/sYjybWe.png" width="350"/> &nbsp;
  <img src="https://i.imgur.com/SuCuUop.png" width="400"/>
</div>

### Call Stack

```txt
 +-----------------+
 |  Call Stack     |  ← Last In, First Out (LIFO)
 |-----------------|
 | funcC()        |  ← Most recent function call
 | funcB()        |  
 | funcA()        |  
 | main()         |  
 +-----------------+
         ↓ (when function completes, it's removed)
 +-----------------+
 |  Global Context |  ← Always at the bottom, remains until program ends
 +-----------------+
```
- The Call Stack is a data structure that JavaScript uses to keep track of function calls. 
- Call Stack follows the `LIFO (Last In, First Out)` principle.
- When a function is called, it is pushed onto the call stack.
- When a function is completed, it is popped from the call stack.
- If the Call Stack becomes too full with function calls and is not cleared, a `Stack Overflow` error occurs.

```js
function recursive() {
    recursive();
}

recursive();
//Uncaught RangeError: Maximum call stack size exceeded
```
- Asynchronous operations (setTimeout, fetch) do not run directly in the Call Stack; they are managed by the Event Loop.

#### **JavaScript Asynchronous Process (4-Step Execution)**  
1. `Call Stack`  
   - JavaScript Engine (like V8) executes code inside the Call Stack.  
   - Functions are pushed onto the stack and removed when execution completes.  

2. `Web APIs`
   - Asynchronous operations (setTimeout, fetch, DOM events) do not stay in the Call Stack.  
   - The browser handles them separately in the Web APIs environment.  

3. `Callback Queue` 
   - Once an async operation is completed, its callback is placed in the Callback Queue.  

4. `Event Loop` 
   - The Event Loop continuously checks if the Call Stack is empty.  
   - If empty, it moves tasks from the Callback Queue back to the Call Stack for execution.  
   - This ensures JavaScript remains non-blocking and runs efficiently.  

```txt
 +-----------------+
 |   Call Stack    |
 |-----------------|
 |   sync tasks    |   ← Function execution happens here
 |                 |
 +-----------------+
         ↓ (if async)
 +-----------------+
 |   Web APIs      |   ← setTimeout, fetch, DOM events handled by browser
 +-----------------+
         ↓ (when async task completes)
 +-----------------+
 | Callback Queue  |   ← Callbacks wait here
 +-----------------+
         ↓ (if Call Stack is empty)
 +-----------------+
 |   Event Loop    |   ← Moves tasks from Callback Queue → Call Stack
 +-----------------+

```
---
## 🌟 Section 3:  Functions & Callbacks 

### How Loops Work in JavaScript?
- JavaScript engines process loops inside the Execution Context, but `loops themselves do not get pushed to the Call Stack`.
- Loops run within a `single Execution Context`, and each iteration performs specific operations.
- If a `function is called inside a loop, that function gets pushed onto the Call Stack` and removed once executed.
- When the loop finishes, the Execution Context is cleared, and memory is freed.
- In `infinite loop, the Call Stack does not overflow but the CPU usage reaches 100%`, freezing the browser.

#### Loops with Asynchronous Code (setTimeout and Loops)
```js
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 1000);
}
// what we expect: 0 1 2
// what happened: 3 3 3
```
**Why does this happen? Let’s analyze it.**
- Each iteration immediately schedules a setTimeout() function in the Web API, but does not execute it right away.
- Since setTimeout is asynchronous, `it does not block the loop`; the loop completes before any setTimeout callback runs.
- By the time the setTimeout callbacks actually execute, the loop has already finished, and i is now 3.
- After 1000ms, the scheduled setTimeout callbacks are moved from the Web API to the callback queue.
- Since `var` does not have block scope, `all three callbacks reference the same i variable`, which is now 3.

```js
//Fixing the Issue: Using let
for (let i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 1000);
}
//Now the output is: 0 1 2
```
**Why does let work?**
- `let has block scope`, so a `new i is created for each iteration`.
- `Each iteration of the loop has its own separate i`, so when setTimeout executes, it references the correct value.

#### In JavaScript, functions are first-class objects. This means:
- **Functions behave like objects**
- You can assign functions to variables.
- You can pass functions as arguments to other functions.
- You can return functions from other functions.
- Functions can have properties and methods just like objects.

- `Higher Order Function` (HOF) is a function that either `takes another function as an argument` (known as a callback function) or `returns a function` as its result.
- `Callback Function` is a function that is passed as an argument to another function and is executed later.
- Callbacks and Higher Order Functions simplify our code and keep it DRY

#### **Pair Programming** 
Pair Programming is a software development technique where **two programmers work together on the same code** at the same time.  

- `Driver`: Actively writes the code.  
- `Navigator`: Reviews each line, gives feedback, and guides the approach.  
- They `switch roles frequently` to ensure collaboration and shared understanding.  

This method helps improve **code quality, knowledge sharing, and problem-solving efficiency**.