
2025-07-02 15:54

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

---
## 🎨 Inline Styling in React – Explained

### 🚫 Can’t Use String CSS Like HTML
In regular HTML you might do:
```html
<button style="background-color: red;">Click</button>
```
But in **React**, you must use an **object with camelCased properties**:

### ✅ Example – Static Inline Styles
```jsx
const styles = {
  backgroundColor: "skyblue",
  borderRadius: "8px",
  padding: "10px",
  color: "white"
};

<button style={styles}>Click Me</button>
```

> 🔸 Style object values are always **strings**.
> 🔸 Properties like `background-color` become `backgroundColor`.

### 🌀 Example – Dynamic Inline Styles
```jsx
function Pad({ isActive }) {
  const styles = {
    backgroundColor: isActive ? "green" : "gray",
    border: isActive ? "2px solid lime" : "1px solid gray"
  };

  return <button style={styles}>Pad</button>;
}
```

### 🧠 Why Use Inline Styles?
- Great for **dynamic UI states**
- Avoids creating many CSS classes for toggles

### ❌ When Not to Use
- Avoid for large style sets — prefer `className` and CSS modules
- No support for pseudo-classes like `:hover`, media queries, etc.


---
## References