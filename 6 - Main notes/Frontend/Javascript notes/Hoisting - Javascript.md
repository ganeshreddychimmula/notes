
2025-07-07 16:33

Status:

Tags: [JavaScript](3%20-%20Tags/JavaScript.md)

---
# Hoisting - Javascript

### 🧠 **What is Hoisting? (The Story Version)**

> Imagine JavaScript as a chef preparing to cook your code. Before actually running any instructions (cooking), it does a **prep round**:
> 
> - It gathers all the **ingredients** (variable and function declarations),
>     
> - Moves them to the **top of the kitchen counter** (the top of the current scope),
>     
> - But crucially, it doesn’t **cook** (assign values or execute logic) yet.
>     
> 
> This early collection step is **hoisting**.

---

### 📖 **Formal Definition**

> **Hoisting** is JavaScript’s behavior of **moving declarations to the top** of their containing scope (global or function) during the **compilation phase**—before the code is executed.

But here’s the catch:

- **Only declarations are hoisted**, **not initializations**.
    

---

### ✅ **What Gets Hoisted?**

|Item|Hoisted?|Notes|
|---|---|---|
|`var` declarations|✅ Yes|Hoisted and initialized to `undefined`|
|`let` and `const`|✅ Yes|Hoisted, but in **Temporal Dead Zone** (TDZ) — cannot be used before declaration|
|Function declarations|✅ Yes|Fully hoisted with the function body|
|Function expressions|❌ No|Only the variable name is hoisted (if `var`), but not the function itself|
|Class declarations|✅ Yes|Hoisted but **not initialized** — using them early throws a ReferenceError|

---

### 🧪 **Code Example: `var` vs `let` vs function**

```js
console.log(x); // undefined
var x = 5;

console.log(y); // ❌ ReferenceError (TDZ)
let y = 10;

greet(); // ✅ "Hello!"
function greet() {
  console.log("Hello!");
}

sayHi(); // ❌ TypeError: sayHi is not a function
var sayHi = function () {
  console.log("Hi!");
};
```

---

### 🔥 Key Takeaways

- `var` is **hoisted and initialized** to `undefined`.
    
- `let` and `const` are **hoisted but not initialized** — they live in the **temporal dead zone** (TDZ).
    
- **Function declarations** are hoisted **entirely**, including their definition.
    
- **Function expressions** are **not hoisted** like full functions.
    


---
## References