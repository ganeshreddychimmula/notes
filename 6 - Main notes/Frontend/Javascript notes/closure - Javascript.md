
2025-07-07 16:55

Status:

Tags:[JavaScript](../../../3%20-%20Tags/JavaScript.md)

---
# closure - Javascript

### 🧠 **What is a Closure? (Story Version)**

> Imagine a **backpack** that a function carries with it.  
> Inside that backpack are **variables from its parent function**, even after the parent is gone.  
> Whenever the inner function runs, it can **reach into the backpack** and use or modify those variables.

That “backpack” is the **closure**.

---

### 📖 **Formal Definition**

> A **closure** is formed when an **inner function remembers and continues to access variables** from its **outer function’s scope**, even **after the outer function has returned**.

In short:  
**"A function + the variables it had access to at the time it was created."**

---

### ✅ **Basic Example**

```js
function outer() {
  let count = 0; // outer variable

  return function inner() {
    count++;
    console.log(`Count is: ${count}`);
  };
}

const counter = outer(); // outer() is called once
counter(); // Count is: 1
counter(); // Count is: 2
counter(); // Count is: 3
```

Here, `inner()` still **remembers** `count`, even though `outer()` has already finished executing. That’s a closure in action.

---

### 💼 **Practical Real-World Use Case: "Private Variables"**

Let’s say you want to **create a counter** with private state—users shouldn’t access or change the counter directly.

```js
function createCounter() {
  let count = 0;

  return {
    increment() {
      count++;
      console.log(count);
    },
    decrement() {
      count--;
      console.log(count);
    },
    getCount() {
      return count;
    }
  };
}

const myCounter = createCounter();
myCounter.increment(); // 1
myCounter.increment(); // 2
console.log(myCounter.getCount()); // 2
myCounter.decrement(); // 1
```

- `count` is **not accessible directly** (e.g. `myCounter.count` is `undefined`)
    
- Only the returned methods can access it — this is **encapsulation using closures**
    

---

### 🔑 Key Takeaways

- Closures help **preserve state** and create **private variables**
    
- They are formed **whenever a function is defined inside another function**
    
- They're essential for things like **event handlers**, **async code**, **functional programming**, and **React hooks (e.g., `useState`)**
    

---

Would you like a visual diagram of closure memory, or want to try a mini coding challenge using closures?

---
## References