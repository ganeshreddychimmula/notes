
2025-08-18 00:54

Status:

Tags: [React](3%20-%20Tags/React.md)

---
# Why not to read or write refs during rendering - React

- Do not write _or read_ `ref.current` during rendering, except for [initialization.](https://react.dev/reference/react/useRef#avoiding-recreating-the-ref-contents) This makes your component’s behavior unpredictable.
	- Reading or writing `ref.current` inside the component's render body (outside `useEffect` or event handlers) can lead to **inconsistent behavior**, because React may call the render function multiple times. Use refs only for **storing values between renders**, not for reactive logic during render.
> 	✅ Safe: `const ref = useRef(0)`  
> 	❌ Risky: `if (ref.current === 0) { doSomething(); }` in render


---

## ✅ Safe Use – Initialization Only During Render

```jsx
import { useRef, useEffect } from "react";

function Counter() {
  const countRef = useRef(0); // safe initialization

  useEffect(() => {
    console.log("This runs after render:", countRef.current);
  }, []);

  return <div>Check console for ref value</div>;
}
```

### ✔ Why This is Safe:

- The ref is initialized with a value (`0`) during render.
    
- Reading or writing to `countRef.current` happens **inside `useEffect`**, which only runs **after** render is complete.
    
- React’s rendering behavior remains predictable.
    

---

## ❌ Risky Use – Reading/Writing Ref During Render

```jsx
function Counter() {
  const countRef = useRef(0);

  // ❌ Don't do this during render
  if (countRef.current === 0) {
    console.log("This is running during render!");
    countRef.current = 1; // mutating during render
  }

  return <div>Rendered with ref value: {countRef.current}</div>;
}
```

### ✘ Why This is Risky:

- You're reading and mutating `countRef.current` **while React is rendering**.
    
- In **Strict Mode**, React may **render your component twice**, causing this logic to run multiple times and lead to unexpected behavior (e.g., side effects, infinite loops).
    
- React expects renders to be **pure**: no mutations, side effects, or non-determinism.
    

---

## ✅ Safer Alternative Using `useEffect`

```jsx
function Counter() {
  const countRef = useRef(0);

  useEffect(() => {
    if (countRef.current === 0) {
      console.log("This runs after mount, safely");
      countRef.current = 1;
    }
  }, []);

  return <div>Rendered with ref value: {countRef.current}</div>;
}
```

### ✔ This is Correct Because:

- ==You defer logic until after the initial render==.
    
- Ensures purity of the render function and avoids double-execution issues in dev mode.
    


---
## References