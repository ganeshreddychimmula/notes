
2025-07-01 11:28

Status:

Tags:[Hooks](Hooks)

---
# Why shouldn't we use hooks inside loops or conditions - React
Let’s break down this important rule about `useState` in React — it's all about **how React tracks state internally**.

## 📌 The Rule

> `useState` is a **Hook**, and Hooks must be called:

- ✅ At the **top level of your component** (not inside `if`, `for`, etc.)
    
- ✅ In the **same order** every time the component renders
    

---

## 🧠 Why This Rule Exists

React uses the ==**order of Hook calls**== to associate each `useState` with its corresponding piece of state.

```jsx
function MyComponent() {
  const [a, setA] = useState(0); // ← 1st hook
  const [b, setB] = useState(0); // ← 2nd hook
}
```

React internally stores them like:

```js
stateArray = [a, b];  // order matters!
```

So if you put `useState` inside a conditional or loop...

```jsx
if (someCondition) {
  const [temp, setTemp] = useState(0); // ❌ this will break React
}
```

...then the **number and order of hooks could change**, and React won’t know which state to assign to which hook.

---

## ❌ Bad Example (violates the rule)

```jsx
function ToggleExample({ showCount }) {
  if (showCount) {
    const [count, setCount] = useState(0); // ❌ BAD: inside condition
  }

  return <div>Toggle something</div>;
}
```

This breaks React’s mental model. React expects `useState` to always be called in the same order, but this one **only runs when `showCount` is true**, so it becomes unpredictable.

---

## ✅ Good Example

```jsx
function ToggleExample({ showCount }) {
  const [count, setCount] = useState(0); // ✅ always called

  return (
    <div>
      {showCount && <p>Count: {count}</p>}
    </div>
  );
}
```

Here, the state is **always created**, but conditionally rendered.

---

## 🔧 What if you really want conditional state?

### ✅ Solution: Extract a new component

```jsx
function ShowCounter() {
  const [count, setCount] = useState(0);
  return <p>Count: {count}</p>;
}

function Parent({ show }) {
  return (
    <>
      {show && <ShowCounter />}
    </>
  );
}
```

> ✅ Now the state only exists if `ShowCounter` is mounted, and React’s rules are respected.

---

## ✅ Summary

|❌ Don’t do this|✅ Do this instead|
|---|---|
|`useState` inside `if`, `for`, `while`|Call it unconditionally at the top level|
|Conditional hook calls|Extract a new component with its own hooks|

---


---
## References