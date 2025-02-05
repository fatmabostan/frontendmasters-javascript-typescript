# 📚 JavaScript Notes - Based on "JavaScript: From First Steps to Professional" by Anjana Vakil (FrontendMasters)

## 🌟 Section 8: Quiz Project  
---  
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

## 🌟 Section 9: Functions  
---  
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

