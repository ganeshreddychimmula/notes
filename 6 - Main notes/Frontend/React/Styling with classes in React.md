
2025-06-25 18:20

Status:

Tags: [React](../../../3%20-%20Tags/React.md) [[Styles]]

---
# Styling with classes in React
Great question! In React, styling with classes is **very similar to HTML/CSS**, but with **one key difference**: the attribute is `className` instead of `class`.

---

## ✅ Basic Syntax

```jsx
function MyComponent() {
  return <div className="my-box">Hello</div>;
}
```

> ⚠️ Why `className`?  
> Because `class` is a **reserved word in JavaScript**, React uses `className` to avoid conflicts.

---

## 🎨 How Styling Works in React

### 1. **With External CSS (Traditional Way)**

```css
/* styles.css */
.my-box {
  background: lightblue;
  padding: 10px;
  border-radius: 8px;
}
```

```jsx
import './styles.css';

function Box() {
  return <div className="my-box">Styled Box</div>;
}
```

---

### 2. **With CSS Modules (Scoped Styling)**

```css
/* Box.module.css */
.box {
  color: red;
}
```

```jsx
import styles from './Box.module.css';

function Box() {
  return <div className={styles.box}>Scoped Box</div>;
}
```

> ✅ CSS Modules automatically scope class names, so they won’t clash with global styles.

---

### 3. **With Tailwind CSS (Utility-First Classes)**

```jsx
function Button() {
  return (
    <button className="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded">
      Click Me
    </button>
  );
}
```

> Tailwind gives you ready-made utility classes to rapidly build custom UIs.

---

### 4. **With Conditional Classes (Dynamic Styling)**

```jsx
function Card({ isActive }) {
  return (
    <div className={isActive ? "card active" : "card"}>
      {isActive ? "Active" : "Inactive"}
    </div>
  );
}
```

> You can also use libraries like `clsx` or `classnames` for cleaner logic:

```bash
npm install clsx
```

```jsx
import clsx from 'clsx';

<div className={clsx("card", isActive && "active")} />
```
---
## 🎨 5. **Styled-Components (CSS-in-JS)**

Styled-components is a **third-party library** that lets you write actual CSS inside your JavaScript files using tagged template literals.

### ✅ Installation:

```bash
npm install styled-components
```

### ✅ Usage:

```jsx
import styled from 'styled-components';

const Button = styled.button`
  background-color: #4caf50;
  color: white;
  padding: 10px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;

  &:hover {
    background-color: #45a049;
  }
`;

function App() {
  return <Button>Styled Button</Button>;
}
```

> ✅ Styles are scoped to the component and can access props for dynamic styling.

---

## 🎨 6. **Inline Styles (JS Object Syntax)**

This method uses the `style` prop with a JavaScript object.

```jsx
function InlineBox() {
  const boxStyle = {
    backgroundColor: 'lightgray',
    padding: '20px',
    borderRadius: '8px',
    color: '#333'
  };

  return <div style={boxStyle}>Inline Styled Box</div>;
}
```

> ⚠️ Note:

- Property names are camelCase (`backgroundColor`, not `background-color`)
    
- Units like `px` must be **manually added** as strings, or numbers will be treated as pixels
    

---

## 🧠 Quick Comparison Table

|Style Method|Scoping|Supports Dynamic Styling|External File?|Notes|
|---|---|---|---|---|
|className (CSS)|Global|❌ Manual|✅ Yes|Simple, but no scoping|
|CSS Modules|Local (scoped)|❌ Manual|✅ Yes|Safe naming, needs import|
|Tailwind CSS|Utility-based|✅ Inline class logic|❌ No|Fast, but can look verbose|
|Styled-Components|Scoped|✅ Built-in|❌ No|Great for theming & animation|
|Inline Styles|Inline|✅ Easy|❌ No|Limited: no pseudo/selectors|

---

## 🔁 Summary

| Method           | Description                          | Use Case                            |
| ---------------- | ------------------------------------ | ----------------------------------- |
| `className`      | React’s way of assigning CSS classes | Always use instead of `class`       |
| External CSS     | Regular stylesheets                  | Simple global styles                |
| CSS Modules      | Locally scoped class names           | Large apps / avoid naming conflicts |
| Tailwind CSS     | Utility-first CSS                    | Rapid styling, consistent spacing   |
| `clsx` / ternary | Conditional class toggling           | Dynamic or interactive UI           |
	
---
## References
