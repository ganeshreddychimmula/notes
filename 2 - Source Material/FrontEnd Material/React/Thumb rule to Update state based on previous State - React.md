
2025-07-01 11:49

Status:

Tags:

---
### ✅ **Thumb Rule for Updating State Based on Previous State in React**

When your **new state value depends on the old one**, **always use the functional form** of the `setState` function (e.g., `setCount(prev => prev + 1)`).

---

### 🔁 Why?

React **batches** state updates for performance. If you call `setState(value)` multiple times in a row without referencing the previous value, **each call uses the same stale snapshot**, leading to bugs.

---

### 🚫 Bad (can lead to unexpected results)

```jsx
setCount(count + 1);
setCount(count + 1);
setCount(count + 1);
```

If `count` was 0, all three lines see `0`, and the final value becomes `1`, not `3`.

---

### ✅ Good (safe and reliable)

```jsx
setCount(prevCount => prevCount + 1);
setCount(prevCount => prevCount + 1);
setCount(prevCount => prevCount + 1);
```

This will correctly result in `count = 3`.

---

### 🧠 Rule of Thumb

> **If your update logic needs the current state value, always use the updater function form.**

---
## References

[Why can't I directly modify a component's state - React](6%20-%20Main%20notes/Frontend/React/Why%20can't%20I%20directly%20modify%20a%20component's%20state%20-%20React.md)