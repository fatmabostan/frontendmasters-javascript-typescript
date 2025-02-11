<div align="center">

# 📚 JavaScript Notes

## Based on "JavaScript: From First Steps to Professional" by Anjana Vakil (FrontendMasters)

</div>

## 🌟 Section 1: Introduction

**What is JS?**

- A dynamic programming language
- Used to modify websites and make them interactive
- Created in 10 days in 1995

---

## 🌟 Section 2: Document Object Model (DOM)

- The `DOM (Document Object Model)` represents a web page as a tree structure. It allows JavaScript to access and modify HTML elements.

<div align="center">
<img src="https://i.imgur.com/JFi6KnN.png" alt="DOM Tree" width="300">
</div>
&nbsp;

- `document`: Represents the entire HTML document
- `document.title`: Page title
- `document.body`: The body element in HTML
- `document.body.children`: All elements within the body
- `document.getElementById("id")`
- `document.getElementsByTagName("h1")`
- `document.getElementsByClassName("class")`
- `document.querySelector(".#")` (Requires a CSS selector)
- `document.querySelectorAll(".#")`
- `.length`: Number of elements
- `.textContent`: Text content of an element
- `.append(" ")`: Adds text to the end of the element's current content

---

## 🌟 Section 3: Values & Data Types

- `typeof value`: Returns the type of a value
- `typeof Infinity`: Returns `"number"` (Yes, JS has a special value named `Infinity`)  
  &nbsp;

| Feature          | **Primitive Values**                                                   | **Objects**                                         |
| ---------------- | ---------------------------------------------------------------------- | --------------------------------------------------- |
| **Definition**   | Immutable, stored by value                                             | Mutable, stored by reference                        |
| **Data Types**   | `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint` | document, arrays, functions, objects, dates, etc.   |
| **Example**      | `let x = 10; let y = "hello";`                                         | `let obj = { name: "Fatma", age: 25 };`             |
| **Memory**       | Stored in stack                                                        | Stored in heap                                      |
| **Copying**      | Creates a new copy                                                     | Copies the reference, not the actual object         |
| **Comparison**   | Compared by value (`===`)                                              | Compared by reference (`===` checks memory address) |
| **Modification** | Cannot be changed (new value assigned instead)                         | Can be modified without reassigning                 |

---

| Feature        | **`null`** 🟢                                                | **`undefined`** 🔴                                   |
| -------------- | ------------------------------------------------------------ | ---------------------------------------------------- |
| **Definition** | Intentional absence of value                                 | A variable declared but not assigned a value         |
| **Type**       | Primitive (but `typeof null` incorrectly returns `"object"`) | `undefined`                                          |
| **When used?** | Assigned by developers to indicate "empty" or "unknown"      | Default value for uninitialized variables            |
| **Example**    | `let x = null;`                                              | `let y;` (automatically `undefined`)                 |
| **Usage Case** | Used when a variable is explicitly set to "no value"         | Happens when JS doesn't assign a value automatically |

&nbsp;

- `.indexOf("H")` or `.indexOf("HA")` Returns the index of the first match; if not found, returns `-1`
- `.includes(" ")` Returns boolean based on whether the string contains the given value
- `.startsWith(" ")` Checks if the string starts with the given value, returns boolean

---

## 🌟 Section 4: Operators

- `typeof` is also an operator.

| Feature              | **`==` (Loose Equality)** 🔵                            | **`===` (Strict Equality)** 🔴                         |
| -------------------- | ------------------------------------------------------- | ------------------------------------------------------ |
| **Type Conversion?** | Yes (converts values to the same type before comparing) | No (compares both **value** and **type** directly)     |
| **Comparison**       | Compares **values only**, converts if necessary         | Compares **both values and types**, no conversion      |
| **Example 1**        | `"5" == 5` → `true` (`"5"` is converted to number)      | `"5" === 5` → `false` (different types)                |
| **Example 2**        | `true == 1` → `true` (`true` is converted to `1`)       | `true === 1` → `false` (boolean vs. number)            |
| **Example 3**        | `null == undefined` → `true`                            | `null === undefined` → `false`                         |
| **Best Practice?**   | ❌ Avoid (can cause unexpected behavior)                | ✅ Always prefer `===` or `!==` for strict comparisons |

---

## 🌟 Section 5: Expressions

| Feature                                    | Expression 🟢                                       | Statement 🔴                                    |
| ------------------------------------------ | --------------------------------------------------- | ----------------------------------------------- |
| **Definition**                             | Uses values and operators, **evaluates to a value** | Performs an action, **does not return a value** |
| **Can be used inside another expression?** | ✅ Yes                                              | ❌ No                                           |
| **Example 1**                              | `5 + 3`                                             | `let x = 5;` (Declares a variable)              |
| **Example 2**                              | `"Hello" + " World"`                                | `if (x > 3) { console.log("Bigger!"); }`        |
| **Example 3**                              | `10 > 5`                                            | `while (x < 10) { x++; }`                       |

```js
// 🟢 Declaration (creating a variable, but no value yet)
let pet;
console.log(pet); // undefined 

// 🔴 Assignment (giving it a value)
pet = "Cat";
console.log(pet); // "Cat" 

// 🎯 Declaration + Assignment in one step
let food = "Pizza";
console.log(food); // "Pizza" 
```

- `Declaration` “Hey, I exist!” (but has no value yet)
- `Assignment` “Now I have a value!” 🎉

---

## 🌟 Section 6: Arrays

- `push()` adds an item to the end
- `.pop()` removes the last item
- `.push()` and `pop()` modify the original array

```js
const snacks = ["🍕", "🍔", "🍟"];
console.log("Original:", snacks); // ["🍕", "🍔", "🍟"]

snacks.push("🌭");
console.log("After push:", snacks); // ["🍕", "🍔", "🍟", "🌭"]

let lastSnack = snacks.pop();
console.log("After pop:", snacks); // ["🍕", "🍔", "🍟"]
console.log("Removed item:", lastSnack); // "🌭"
```
Arrays are mutable so their elements can be changed, but their reference (memory location) stays the same.

<div align="center">
<img src="https://i.imgur.com/5jva0tg.png" width="300">
</div>
&nbsp;

- `.sort()` Sorts elements as STRINGS by default
- `.sort()` modifies the original array

```js
const numbers = [10, 2, 8, 1, 20];
numbers.sort();
console.log(numbers); // ❌ [1, 10, 2, 20, 8] (Wrong order!)

// 🔴 Fixing sort() for numbers
numbers.sort((a, b) => a - b);
console.log(numbers); // ✅ [1, 2, 8, 10, 20] (Correct order)

// 🍕 Sorting strings alphabetically
const snacks = ["🍕", "🍔", "🍟", "🌭"];
snacks.sort();
console.log(snacks); // ["🌭", "🍔", "🍕", "🍟"] (Sorted by Unicode)
```

- `.concat()` Combines arrays without modifying them
- `.join()` Converts an array into a string

```js
const arr1 = ["🍕", "🍔"];
const arr2 = ["🍟", "🌭"];

const allSnacks = arr1.concat(arr2);
console.log("Original:", arr1, arr2); // ["🍕", "🍔"] ["🍟", "🌭"] (Unchanged)
console.log("Concatenated:", allSnacks); // ["🍕", "🍔", "🍟", "🌭"] 

const snackString = allSnacks.join(" + ");
console.log("Joined:", snackString); // "🍕 + 🍔 + 🍟 + 🌭"
```

---

## 🌟 Section 7: Objects
- Objects are mutable so their property can be changed, but their reference (memory location) stays the same.
```js
//Cat Object
const cat = {
    //Property (Key: Value)
  name: "Whiskers", 
  age: 3,
  isFriendly: true,
  favoriteFoods: ["🐟", "🥩", "🧀"],
  meow: function() {
    return "Meow! 🐱";
  }
    //object method
  introduce() {
    return `Hi, I'm ${this.name}, and I'm ${this.age} years old!`;
  }
};

console.log(cat.name); // "Whiskers"
console.log(cat.age); // 3
console.log(cat.favoriteFoods[0]); // "🐟"
console.log(cat.meow()); // "Meow! 🐱"
console.log(cat.introduce()); // "Hi, I'm Whiskers, and I'm 3 years old!"
```

### If strings are primitive data types, why do they have built-in functions like objects?
Primitive values (like strings, numbers, and booleans) are not objects, but they temporarily behave like objects when you try to use a method.
- When you call a method on a string (e.g., "hello".toUpperCase()), JavaScript automatically wraps the string in a temporary String object behind the scenes.
- This temporary object allows access to built-in methods (toUpperCase(), slice(), etc.).
- Once the operation is complete, JavaScript discards the temporary object, and the original primitive value remains unchanged.

### In JavaScript, arrays are actually a special type of object.
- Arrays are objects but are optimized for ordered data.
- They use numeric indexes instead of named keys.

```js
// Object
const person = {
  name: "Fatma",
  age: 25
};
// indexed with string
console.log(person["name"]); // "Fatma"

// Array
const fruits = ["Apple", "Banana", "Cherry"];
// indexed with number
console.log(fruits[0]); // "Apple"

```

---

## 🌟 Section 8: Quiz Project

### Different Ways to Define Object Properties:

#### 1️⃣ Using Quoted Property Names (for properties with spaces)

If a property name contains spaces, it must be enclosed in quotes.

```javascript
let myObject = {
  "my longer property": "and this is the value",
};
```

❌ You can't use: `myObject.my longer property`  
✅ You can use: `myObject["my longer property"]`

#### 2️⃣ Using Standard Property Names (without spaces)

If the property name is a valid identifier (no spaces or special characters), you can use **dot notation** or **bracket notation**.

```javascript
let myAnotherObject = {
  myProperty: "value",
};
```

✅ You can use: `myAnotherObject.myProperty`  
✅ You can also use: `myAnotherObject["myProperty"]`

---

## 🌟 Section 9: Functions

- **Values** are things.
- **Variables** point to things.
- **Functions** do things.

### Declaring a Function:

```javascript
function add3(x, y, z) {
  return x + y + z;
}

const yell = function (saying) {
  return saying.toUpperCase();
};
```

#### Syntax:

```javascript
function functionName(parameters) {}
functionName(arguments);
```

```javascript
function doesThisWork("it is a value") {} // ❌ Missing formal parameter
function doesThisWork(1WeirdVariable!) {} // ❌ Identifier starts with a number or invalid character
```

- `add3(5, 4)` → ✅ 5, 4, undefined. Returns `NaN` (Not a Number).
- `typeof NaN` is ironically `"number"`.
- `Math.random("expected")` → ✅ JavaScript ignores unexpected arguments.

- In JavaScript, **functions always return something**.
- If there is no `return` statement, the function returns `undefined` by default.

### **_Arrow Functions_**

- Quick way to create small simple functions.
- Create unnamed, anonymous functions.

```javascript
const add = (x, y) => x + y;
```

### **_Scope of Variables_**

- Scope determines where variables are "in play".
- Scopes are **_nested_** within the program.
- The widest scope is **_global scope_**.
  &nbsp;

<div align="center">
<img src="https://i.imgur.com/oBD70G0.png" width="340">&nbsp;
<img src="https://i.imgur.com/oioB8GM.png" width="300">
</div>

```javascript
global scope

function lookScope(){
    function scope
}

if / loop{
    block scope
}
```

- From global scope, we can't see in.
- Inner scope can see out.

&nbsp;

| **Aspect**                    | **var**                                              | **let**                                                    | **const**                                                  |
| ----------------------------- | ---------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| **1. Scope Differences**      | Function Scope only (does not work with block scope) | Block Scope (accessible only within the block)             | Block Scope (accessible only within the block)             |
| **2. Mutability Differences** | Can be reassigned                                    | Can be reassigned                                          | Cannot be reassigned (immutable)                           |
| **3. Hoisting Differences**   | Hoisted and initialized with `undefined`             | Hoisted but cannot be accessed before initialization (TDZ) | Hoisted but cannot be accessed before initialization (TDZ) |

---

## 🌟 Section 10: Event Listeners

- `.addEventListener()` listens for events on a DOM element.

```javascript
document.addEventListener("event", callbackFunction / handlerFunction);
```

- JS passes an `event` object to the handler function with information about the event. If you accept this as a parameter, you can use it to get details.

```javascript
document.addEventListener("click", (event) => {
  console.log(event.target);
});
```

---

## 🌟 Section 11: Conditionals & Loops

```javascript
if(condition){
    //do something
} else if{
    //do something
} else {
    //do something
}
```

- `null / undefined / "" (empty string)` => false
- `empty array []` => true

### **_Ternary Operator_**

```js
condition ? valueIfTrue : valueIfFalse;
```

```js
for (let rep = 0; rep < 10; rep++) {
  console.log(`Iteration: ${rep}`);
}
```

```js
for (let n of array) {
  console.log(n);
}
```

---

## 🌟 Section 12: Map & Filter & Spread

`reduce`

- Reduces an array to a single value by applying a function to each element.
- Takes a callback function
- Returns last callback value

```javascript
const totalCost = cart.reduce((total, item) => total + item.price, 0);
console.log(totalCost); // Output: 10
```

`map`

- Creates a new array by applying a function to each element.

```javascript
const numbers = [1, 2, 3];
const doubled = numbers.map((num) => num * 2);
console.log(doubled); // Output: [2, 4, 6]
```

`forEach`

- Executes a provided function once for each array element.
- Does not return a new array.

```javascript
const numbers = [1, 2, 3];
numbers.forEach((num) => console.log(num));
// Output: 1, 2, 3
```

`filter`

- Creates a new array with all elements that pass the test.

```javascript
const numbers = [1, 2, 3, 4, 5];
const evens = numbers.filter((num) => num % 2 === 0);
console.log(evens); // Output: [2, 4]
```

### **Spread Operator (...)**

- use this to expand an array into another array

```js
const avengers = ["Iron Man", "Thor", "Hulk"];
const guardians = ["Star-Lord", "Gamora", "Rocket"];
const ultimateTeam = [...avengers, ...guardians, "Ant-Man"];
```

---

## 🌟 Section 13: setTimeout

- JS can usually run program "synchronously"
- JS single-threaded

```javascript
//This task runs some time later, "asynchronously"
console.log("This will print first");
setTimeout(() => console.log("This will print third"), 1000); //JS add the slow task to a "TODO list" and keeps on running program
console.log("This will print second.");
```

---

## 🌟 Section 14: Data Fetching & Promises

- https://dog.ceo/api/breeds/image/random
- baseURL/endpoint/endpoint/...?query=writeSomething&query=writeSomething
- Promises are "asynchronous"

```javascript
fetch("https://dog.ceo/api/breeds/image/random");
// Promise { <state>: "pending" }
```

- A `Promise` means: I promise I'm going to get you this value, but I don't have it yet.
- `Promise` is a construct in JS that let's us represent a value, we don't have yet.
  **_Promises can be in 3 possible states:_**
- `pending`: still waiting for the value
- `fulfilled(resolved)`: finally got the value
- `rejected`: sorry couldn't get the value

JS doesn’t wait for the pending Promise and keeps running the code. However, without the data, our program wouldn’t be meaningful. So, we use `await` to tell JavaScript to wait.

```javascript
let response = await fetch("https://dog.ceo/api/breeds/image/random");
// wait for the promise to be done and give me the value of the promise
// returns response object
```

- The response object has a body(ReadableStream), but we still can't use it directly.
- We need to use `.json()` to convert it from bytes to readable data.

```javascript
const data = await response.json();
// We must wait for the conversion process, so we need to use "await"
```

---

## 🌟 Section 15: Destructuring Data

```javascript
const avengers = {
  ironMan: "Tony Stark",
  captainAmerica: "Steve Rogers",
  thor: "Thor Odinson",
  hulk: "Bruce Banner",
};
// Destructuring
const { ironMan, captainAmerica, thor, hulk } = avengers;
```

```javascript
const colors = ["Red", "Green", "Blue"];

// Destructuring the array
const [firstColor, secondColor, thirdColor] = colors;

console.log(firstColor); // "Red"
console.log(secondColor); // "Green"
console.log(thirdColor); // "Blue"
```

```javascript
const fruits = ["Apple", "Banana", "Cherry", "Mango", "Peach"];

// Get the first two elements, store the rest in "otherFruits"
const [first, second, ...otherFruits] = fruits;

console.log(first); // "Apple"
console.log(second); // "Banana"
console.log(otherFruits); // ["Cherry", "Mango", "Peach"]
```

---

## 🌟 Section 16: Async

We must declare a function as `async` when we use `await` inside it.

```javascript
async function fetchRandomCat() {
  console.log("Fetching a random cat... 🐱");
  const response = await fetch("https://api.thecatapi.com/v1/images/search");
  const data = await response.json();
  const catImageUrl = data[0].url;
  console.log("Here's your cat! 🎉:", catImageUrl);
}

const myCatImg = await fetchRandomCat();
```

---

## 🌟 Section 17: Modules

```javascript
//default
<script type="text/javascript"></script>
```

```js
<script type="module"></script>
```

| Feature               | Modules (`type="module"`)                            | Scripts (`<script>`)                                                                 |
| --------------------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------ |
| **Import/Export**     | ✅ Supports `import` and `export`                    | ❌ Not supported                                                                     |
| **Scope**             | ✅ Has its own scope                                 | ❌ Uses global scope (variables are added to window, can be accessed in the console) |
| **Strict Mode**       | ✅ Always enabled                                    | ❌ Not enabled by default                                                            |
| **Execution Order**   | ✅ Deferred by default                               | ❌ Executes immediately (unless `defer`/`async` is used)                             |
| **Type Declaration**  | ✅ Requires `<script type="module">`                 | ❌ Uses a normal `<script>` tag                                                      |
| **File Loading**      | ✅ Uses `import` to load other modules               | ❌ Dependencies must be manually included                                            |
| **Top-level `this`**  | ❌ `this` is `undefined`                             | ✅ `this` refers to `window`                                                         |
| **Top-level `await`** | ✅ Supported (`await` can be used outside functions) | ❌ Not supported (must be inside `async function`)                                   |

### **_Debugging_**

- `console.log()`, `console.warn()`, `console.error()` is one way to understand what's happening when your program runs.
- Browser's debugger: write `debugger;` or use `breakpoint`

### **_Error Handling_**

```js
try {
  //something might throw an error
} catch (error) {
  //catch error
}
```
