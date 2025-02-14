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