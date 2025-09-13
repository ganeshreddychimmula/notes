
2025-07-01 12:08

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

---
# Batching in React - Understanding how react efficiently updates UI
 **Batching** in React — it's a super important concept for understanding how React efficiently updates the UI.

---

## 🧠 What is Batching?

> **Batching** is when React **groups multiple state updates together** and processes them **in a single re-render**, instead of one re-render per update.

---

### ✅ Why React Does This:

- To improve **performance**
    
- Avoid unnecessary re-renders
    
- Ensure **UI updates only once**, even if multiple state changes happen together
    

---

## 🔁 Without Batching (conceptually):

```jsx
setCount(1); // re-render
setName("Alice"); // another re-render
setAge(30); // another re-render
```

That would be **3 re-renders** — inefficient and wasteful.

---

## ✅ With Batching:

```jsx
setCount(1);
setName("Alice");
setAge(30);
```

✅ React **batches all 3 updates together**  
✅ Only **1 re-render** happens — after all updates are processed.

---

## 📦 Batching in Action Example:

```jsx
function Example() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState('');

  function handleClick() {
    setCount(count + 1);
    setText('Updated!');
  }

  return (
    <>
      <p>Count: {count}</p>
      <p>Text: {text}</p>
      <button onClick={handleClick}>Update Both</button>
    </>
  );
}
```

✅ Clicking the button causes **both state updates** — but React only re-renders **once**.

---

## ⚠️ When Batching Doesn't Happen (pre-React 18 or outside React scope)

Before React 18, batching only worked inside event handlers (like `onClick`).  
It didn’t batch updates in:

- `setTimeout`
    
- `fetch().then(...)`
    

---

### ✅ React 18+ Fixes That

React 18 introduced **automatic batching everywhere** — even in async callbacks:

```jsx
setTimeout(() => {
  setCount(c => c + 1);
  setText("Async update");
  // ✅ Still batched!
}, 1000);
```

---

## 🧠 TL;DR

|Concept|Explanation|
|---|---|
|What is it?|Combining multiple state updates into 1 render|
|Why?|Better performance and smoother UI|
|When?|Always in React 18+ (incl. async code)|
|Before React 18|Only inside event handlers (like `onClick`)|

---

 
## React handles **multiple event handlers** using **batched updates**, especially in React 18 and later.

Let’s break it down:

---

## 🧠 What happens when **multiple event handlers** run?

React will:

- Execute all the event handlers
    
- Collect any `setState()` calls made
    
- Batch all those updates into **one single re-render**
    

> ✅ This improves performance and ensures the UI is updated only once — **after all logic finishes**.

---

### ✅ Example: Multiple Event Handlers

```jsx
function ParentComponent() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState('');

  const handleClick1 = () => {
    setCount(prev => prev + 1);
    console.log('Click 1 finished');
  };

  const handleClick2 = () => {
    setText('Updated!');
    console.log('Click 2 finished');
  };

  const handleBoth = () => {
    handleClick1();
    handleClick2();
    console.log('All done');
  };

  return (
    <>
      <p>{count}</p>
      <p>{text}</p>
      <button onClick={handleBoth}>Run All</button>
    </>
  );
}
```

---

### 🔄 What happens when you click the button?

- React runs `handleBoth()`
    
- Inside it, `handleClick1()` and `handleClick2()` are both run
    
- Each one calls `setState()`
    
- ✅ React **batches** the updates
    
- ✅ Only **one re-render** happens **after all** handlers finish
    

---

## ⚠️ What if you break out of React context?

In older versions of React (or with custom logic), updates in **async code** like `setTimeout`, `fetch()`, etc. were **not batched** by default:

```js
setTimeout(() => {
  setCount(c => c + 1);
  setText('async');
}, 1000);
```

### ✅ In React 18:

Even these are batched automatically unless you turn off concurrent features.

---

## 🧠 Summary

| Scenario                      | Re-renders             |
| ----------------------------- | ---------------------- |
| Multiple handlers, same click | ✅ 1 total              |
| Each handler with `setState`  | ✅ Still 1              |
| React batches all updates     | ✅ Yes                  |
| Pre-React 18 (async cases)    | ❌ Might not be batched |


---
## References
[Queueing a Series of State Updates - React](Queueing%20a%20Series%20of%20State%20Updates%20-%20React.md)