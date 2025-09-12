
2025-07-07 18:01

Status: 

Tags: [JavaScript](3%20-%20Tags/JavaScript.md) 

---
# Truthy and Falsy Values - JavaScript

Let’s dive into the concept of **truthy** and **falsy** values in JavaScript — a key concept that helps you understand how conditions work in `if`, `while`, `&&`, `||`, etc.

---

### 🧠 **What Are Truthy and Falsy Values?**

In JavaScript, **every value** is either:

- **Truthy** → Treated as `true` when evaluated in a boolean context
    
- **Falsy** → Treated as `false` in a boolean context
    

> 💡 In `if (value)` or `while (value)`, JavaScript internally converts `value` to a boolean using **type coercion**.

---

### 🚫 Falsy Values (Only 7 of them!)

There are **exactly 7 falsy values** in JavaScript:

|Value|Type|Notes|
|---|---|---|
|`false`|Boolean|Literal false|
|`0`|Number|Zero|
|`-0`|Number|Negative zero (rare)|
|`0n`|BigInt|BigInt zero|
|`""`|String|Empty string|
|`null`|Null|No value|
|`undefined`|Undefined|Not assigned|
|`NaN`|Number (Invalid)|“Not a Number”|

✅ **Everything else** is considered **truthy**.

---

### ✅ Truthy Examples

All of these will evaluate as `true`:

```js
if ("hello")     // ✅ true
if (42)          // ✅ true
if ([])          // ✅ true
if ({})          // ✅ true
if ("0")         // ✅ true
if (Infinity)    // ✅ true
```

> Even empty arrays `[]` and empty objects `{}` are truthy!

---

### 🔍 Practical Example

```js
let userInput = "";

if (userInput) {
  console.log("You entered:", userInput);
} else {
  console.log("No input given."); // This will run because "" is falsy
}
```

---

### 🧪 Testing with Boolean()

You can test what’s truthy or falsy using the `Boolean()` function:

```js
Boolean("")       // false
Boolean("hello")  // true
Boolean(0)        // false
Boolean([])       // true
```

---

### 🧠 Key Takeaway

> **Falsy values (7 total)** are special and predictable.  
> Use `Boolean(value)` to test them. Everything else — strings, arrays, objects, numbers (except `0`/`NaN`) — are **truthy**.

---

## References