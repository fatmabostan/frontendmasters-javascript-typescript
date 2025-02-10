<div align="center">

# 📚 JavaScript Notes 
## Based on "JavaScript: From First Steps to Professional" by Anjana Vakil (FrontendMasters)

</div>

---

## 🌟 Section 8: Quiz Project
### Different Ways to Define Object Properties:  

#### 1️⃣ Using Quoted Property Names (for properties with spaces)  
If a property name contains spaces, it must be enclosed in quotes.  
```javascript
let myObject = {
    "my longer property": "and this is the value"
};
```
❌ You can't use: `myObject.my longer property`  
✅ You can use: `myObject["my longer property"]`  

#### 2️⃣ Using Standard Property Names (without spaces)  
If the property name is a valid identifier (no spaces or special characters), you can use **dot notation** or **bracket notation**.  
```javascript
let myAnotherObject = {
    myProperty: "value"    
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

const yell = function(saying){
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

### ***Arrow Functions***  
- Quick way to create small simple functions.  
- Create unnamed, anonymous functions.  

```javascript
const add = (x, y) => x + y;
```

### ***Scope of Variables***  
- Scope determines where variables are "in play".
- Scopes are ***nested*** within the program.
- The widest scope is ***global scope***.

&nbsp;

---
<div align="center">
<img src="https://i.imgur.com/oBD70G0.png" width="340">&nbsp;
<img src="https://i.imgur.com/oioB8GM.png" width="300">
</div>

---

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

| **Aspect**                    | **var**                                  | **let**                                  | **const**                                |
|-------------------------------|------------------------------------------|------------------------------------------|------------------------------------------|
| **1. Scope Differences**       | Function Scope only (does not work with block scope) | Block Scope (accessible only within the block) | Block Scope (accessible only within the block) |
| **2. Mutability Differences**  | Can be reassigned                        | Can be reassigned                        | Cannot be reassigned (immutable)         |
| **3. Hoisting Differences**    | Hoisted and initialized with `undefined` | Hoisted but cannot be accessed before initialization (TDZ) | Hoisted but cannot be accessed before initialization (TDZ) |

---

## 🌟 Section 10: Event Listeners

- `.addEventListener()` listens for events on a DOM element.

```javascript
document.addEventListener("event", callbackFunction/handlerFunction);
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

### ***Ternary Operator***  
```js
condition ? valueIfTrue : valueIfFalse;
```

```js
for (let rep = 0; rep < 10; rep++){
    console.log(`Iteration: ${rep}`);
}
```
```js
for(let n of array){
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
const doubled = numbers.map(num => num * 2);
console.log(doubled); // Output: [2, 4, 6]
```

`forEach`
- Executes a provided function once for each array element.
- Does not return a new array.
```javascript
const numbers = [1, 2, 3];
numbers.forEach(num => console.log(num));
// Output: 1, 2, 3
```

`filter`
- Creates a new array with all elements that pass the test.
```javascript
const numbers = [1, 2, 3, 4, 5];
const evens = numbers.filter(num => num % 2 === 0);
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
setTimeout(() => console.log("This will print third"),1000); //JS add the slow task to a "TODO list" and keeps on running program
console.log("This will print second.")
```
---

## 🌟 Section 14: Data Fetching & Promises
- https://dog.ceo/api/breeds/image/random 
- baseURL/endpoint/endpoint/...?query=writeSomething&query=writeSomething
- Promises are "asynchronous"
```javascript
fetch("https://dog.ceo/api/breeds/image/random")
// Promise { <state>: "pending" }
```
- A `Promise` means: I promise I'm going to get you this value, but I don't have it yet.
- `Promise` is a construct in JS that let's us represent a value, we don't have yet.
***Promises can be in 3 possible states:***
- `pending`: still waiting for the value
- `fulfilled(resolved)`: finally got the value
- `rejected`: sorry couldn't get the value

JS doesn’t wait for the pending Promise and keeps running the code. However, without the data, our program wouldn’t be meaningful. So, we use `await` to tell JavaScript to wait.

```javascript
let response = await fetch("https://dog.ceo/api/breeds/image/random")
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
  hulk: "Bruce Banner"
};
// Destructuring 
const { ironMan, captainAmerica, thor, hulk } = avengers;
```
```javascript
const colors = ["Red", "Green", "Blue"];

// Destructuring the array
const [firstColor, secondColor, thirdColor] = colors;

console.log(firstColor);  // "Red"
console.log(secondColor); // "Green"
console.log(thirdColor);  // "Blue"
```
```javascript
const fruits = ["Apple", "Banana", "Cherry", "Mango", "Peach"];

// Get the first two elements, store the rest in "otherFruits"
const [first, second, ...otherFruits] = fruits;

console.log(first);       // "Apple"
console.log(second);      // "Banana"
console.log(otherFruits); // ["Cherry", "Mango", "Peach"]
```
---

## 🌟 Section 16: Async
We must declare a function as `async` when we use `await` inside it.

```javascript
async function fetchRandomCat() {
    console.log("Fetching a random cat... 🐱");
    const response = await fetch('https://api.thecatapi.com/v1/images/search');
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
<script type="text/javascript">  
</script>                         
```            
```js
<script type="module">
</script>
```                    

| Feature         | Modules (`type="module"`) | Scripts (`<script>`) |
|---------------|----------------------|----------------|
| **Import/Export** | ✅ Supports `import` and `export` | ❌ Not supported |
| **Scope** | ✅ Has its own scope | ❌ Uses global scope (variables are added to window, can be accessed in the console) |
| **Strict Mode** | ✅ Always enabled | ❌ Not enabled by default |
| **Execution Order** | ✅ Deferred by default | ❌ Executes immediately (unless `defer`/`async` is used) |
| **Type Declaration** | ✅ Requires `<script type="module">` | ❌ Uses a normal `<script>` tag |
| **File Loading** | ✅ Uses `import` to load other modules | ❌ Dependencies must be manually included |
| **Top-level `this`** | ❌ `this` is `undefined` | ✅ `this` refers to `window` |
| **Top-level `await`** | ✅ Supported (`await` can be used outside functions) | ❌ Not supported (must be inside `async function`) |

### ***Debugging***
- `console.log()`, `console.warn()`, `console.error()` is one way to understand what's happening when your program runs.
- Browser's debugger: write `debugger;` or use `breakpoint`

### ***Error Handling***
```js
try{
    //something might throw an error
} catch(error){
    //catch error
}
```