
2025-07-07 18:25

Status:

Tags: [[JavaScript]]

---
# Arrow Function and how it is different from others - Javascript
## 🏹 What is an Arrow Function?

> An **arrow function** is a shorthand syntax introduced in ES6 for writing anonymous functions.

### ✅ Syntax:

```js
// Regular function
function add(a, b) {
  return a + b;
}

// Arrow function
const add = (a, b) => a + b;
```

---

## 🔍 Key Differences Between Arrow Functions and Regular Functions

| Feature                 | Regular Function                     | Arrow Function                       |
| ----------------------- | ------------------------------------ | ------------------------------------ |
| **Syntax**              | Verbose                              | Shorter, cleaner                     |
| **`this` keyword**      | Dynamic (depends on how it’s called) | Lexical (inherits from parent scope) |
| **`arguments` object**  | ✅ Available                          | ❌ Not available                      |
| **Constructor support** | ✅ Can use `new`                      | ❌ Cannot be used as constructor      |
| **Implicit return**     | ❌ No                                 | ✅ Yes (if one-line, no `{}` needed)  |
| **Named functions**     | Can be named or anonymous            | Always anonymous (unless assigned)   |
|                         |                                      |                                      |
|                         |                                      |                                      |

---

### 🎯 `this` Behavior Example

```js
function regularFunc() {
  console.log("Regular:", this);
}

const arrowFunc = () => {
  console.log("Arrow:", this);
};

const obj = {
  method: regularFunc,
  arrow: arrowFunc
};

obj.method(); // Regular: obj (because `this` is dynamic)
obj.arrow();  // Arrow: window/global (because `this` is inherited from creation scope)
```

🔑 **Arrow functions don’t bind their own `this`**, they use the value from their **defining context**, not from where they're called.

---

### ⚠️ When Not to Use Arrow Functions

Avoid using arrow functions when:

- You need access to `this`, `super`, or `arguments`
    
- You’re writing a method in a class or object (they won't bind `this` properly)
    
- You need a constructor function
    

---

### ✅ Use Arrow Functions When:

- Writing short, simple functions
    
- Inside array methods like `map`, `filter`, or `reduce`
    
- To preserve `this` in callbacks (e.g., inside a `setTimeout`)
    

---

### 🔁 Example in React

```js
// Good use in React component
const handleClick = () => {
  setCount(count + 1); // `this` is naturally preserved
};
```

---

## 🧠 Summary

|Arrow Function|Regular Function|
|---|---|
|Concise syntax|Verbose|
|Lexical `this`|Dynamic `this`|
|No `arguments` object|Has `arguments`|
|No `new`/constructor|Can be used as constructor|

---
## References