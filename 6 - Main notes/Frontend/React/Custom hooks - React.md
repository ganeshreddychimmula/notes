
2025-08-18 13:07

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

---
# Custom hooks - React
https://react.dev/learn/reusing-logic-with-custom-hooks#

## 🧠 What Are Custom Hooks? 

A **custom hook** is a JavaScript function whose name starts with `use` and that **uses built-in React hooks** inside it (like `useState`, `useEffect`, `useRef`, etc.).

They allow you to **reuse logic between components** while keeping code clean, readable, and modular.

> Think of custom hooks as a way to extract and reuse logic — like forms, timers, animations, or API calls — across components.

---

## ✅ Why Use Custom Hooks?

|Benefit|Explanation|
|---|---|
|♻️ Reusability|Share logic without duplicating code|
|🧼 Separation of Concerns|Keep component files focused on UI|
|🧪 Testability|Easier to write tests for isolated logic|
|⚙️ Composability|Combine multiple hooks together|

---

## 🧪 Basic Custom Hook Example

```jsx
// useCounter.js
import { useState } from 'react';

export function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => setCount(c => c + 1);
  const decrement = () => setCount(c => c - 1);
  const reset = () => setCount(initialValue);

  return { count, increment, decrement, reset };
}
```

### Using It in a Component

```jsx
import { useCounter } from './useCounter';

function Counter() {
  const { count, increment, decrement, reset } = useCounter(5);

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}
```

---

## 🔁 Custom Hook with Side Effects

```jsx
// useDocumentTitle.js
import { useEffect } from 'react';

export function useDocumentTitle(title) {
  useEffect(() => {
    document.title = title;
  }, [title]);
}

// Usage
function Page() {
  useDocumentTitle("My Page");
  return <h1>Welcome</h1>;
}
```

---

## 🧩 Custom Hook for Fetching Data

```jsx
// useFetch.js
import { useState, useEffect } from 'react';

export function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    setLoading(true);
    fetch(url)
      .then(res => res.json())
      .then(data => {
        setData(data);
        setLoading(false);
      });
  }, [url]);

  return { data, loading };
}

// Usage
function UserList() {
  const { data, loading } = useFetch("https://api.example.com/users");
  if (loading) return <p>Loading...</p>;
  return <ul>{data.map(user => <li key={user.id}>{user.name}</li>)}</ul>;
}
```

---

## 🧠 Key Principles of Custom Hooks

1. **Name must start with `use`**
    
    - This is how React knows it’s a hook.
        
2. **Can call other hooks inside**
    
    - `useState`, `useEffect`, `useRef`, or even other custom hooks.
        
3. **No conditional usage of hooks**
    
    - Must follow the **Rules of Hooks**.
        

---

## 🔗 Related Concepts

### 1. **Built-in Hooks**

Custom hooks are built using these:

- `useState`, `useEffect`, `useRef`, `useMemo`, `useContext`, etc.
    

### 2. **Render Props vs. Custom Hooks**

|Feature|Render Props|Custom Hooks|
|---|---|---|
|UI control|Passed as children|Separated from logic|
|Composition|Verbose with nesting|Clean and scalable|
|Preferred Today|❌ Less common|✅ Recommended|

### 3. **Higher-Order Components (HOC)**

HOCs were used to share logic before hooks. Custom hooks now make this cleaner.

---

## ✅ When to Create a Custom Hook

|Situation|Create Hook?|
|---|---|
|Using same state logic in multiple places|✅ Yes|
|Managing timers, animations, forms, etc.|✅ Yes|
|Just wrapping one hook call|❌ Not needed|
|One-off logic in a single component|❌ Not needed|

---

## 🧾 Summary

- Custom hooks help you abstract and reuse logic across components.
    
- They improve readability, modularity, and maintainability.
    
- Built using built-in hooks, and follow the same rules.
    
- Ideal for forms, fetching, timers, toggles, and more.
    


---
## ✅ **Use Custom Hooks When...**

### 1. **You’re Reusing Logic Across Multiple Components**

- Examples:
    
    - Fetching data from an API
        
    - Form validation or state
        
    - Scroll or resize event tracking
        

> 📌 Use custom hooks to **DRY** up your code and avoid duplicating logic.

---

### 2. **You Want to Extract Complex Logic from a Component**

- Helps break down large components into smaller, readable parts.
    
- Keeps **UI and logic separate**.
    

> ✅ Improves maintainability and testability.

---

### 3. **You Need to Share Side Effects (e.g. `useEffect`)**

- Use when multiple components perform the same side effects, like:
    
    - Setting `document.title`
        
    - Managing intervals/timers
        
    - Subscribing to events or sockets
        

---

### 4. **You’re Managing Local, Encapsulated State**

- Example: toggles, counters, modal visibility
    

```js
const { isOpen, toggle } = useToggle()
```

> 🔄 Perfect for extracting clean logic around `useState`.

---

### 5. **You Want to Abstract Third-Party or Low-Level Hooks**

- Wrap logic around things like:
    
    - IntersectionObserver
        
    - Local storage
        
    - Media queries
        
    - External libraries (e.g., Firebase, Apollo)
        

---

## ❌ **Avoid Custom Hooks When...**

|Situation|Better Approach|
|---|---|
|Logic used only once|Inline it in the component|
|Only calling one built-in hook|No need to abstract|
|Creating UI elements or components|Use regular components|

---

## 🧾 Summary

|Use Custom Hook When...|Example|
|---|---|
|You repeat logic in multiple places|useFetch, useForm|
|You need side effects reused cleanly|useDocumentTitle, useTimer|
|You want to encapsulate logic, not UI|useAuth, useScroll|
|You want cleaner component files|Split logic into hooks|


---
## References