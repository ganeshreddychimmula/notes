
2025-07-01 17:05

Status:

Tags:

---
# Conditional Rendering and Ternary operator in React
## Conditional Rendering in React – Explained

### 💡 What is Conditional Rendering?
Conditional rendering in React means **displaying components or elements only if certain conditions are met**.

Think of it as React’s way of saying:
> "If this is true, show it. If not, skip it."

---

### ✅ Example: Basic Conditional Rendering
```jsx
import React from "react"

export default function Joke(props) {
  const [isShown, setIsShown] = React.useState(false);

  function toggleShown() {
    setIsShown(prevShown => !prevShown);
  }

  return (
    <div>
      {props.setup && <h3>{props.setup}</h3>}
      {isShown && <p>{props.punchline}</p>}
      <button onClick={toggleShown}>Show punchline</button>
      <hr />
    </div>
  );
}
```

- If `props.setup` exists, the heading will be shown.
- `isShown` controls whether or not to display the punchline.

---

### 🤔 Why Does `&&` Work in JSX?

```js
if (true && false) {
  // false — does not run
}
```

In JavaScript, `&&` (logical AND):
- **Evaluates the left side first**
- If the **left is truthy**, it evaluates and returns the **right**
- If the **left is falsy**, it skips the right and returns **false** immediately

This is called **short-circuiting**.

### ✅ In JSX:
```jsx
{isShown && <p>{props.punchline}</p>}
```
- If `isShown` is true → React renders the `<p>` tag
- If `isShown` is false → React renders **nothing**

---

### 🆚 Showing Two Different Things with `&&`
```jsx
{unreadMessages.length > 0 && (
  <h1>You have {unreadMessages.length} unread messages!</h1>
)}

{unreadMessages.length === 0 && (
  <p>You have no unread messages</p>
)}
```

- ✅ This works, but it’s **redundant** and a bit verbose

---

### ✨ Solution: Ternary Operator
```jsx
{
  unreadMessages.length > 0
    ? <h1>You have {unreadMessages.length} unread messages!</h1>
    : <p>You have no unread messages</p>
}
```

- Cleaner
- One line to handle both options

#### 🧪 Another Example
```jsx
const isLoggedIn = true;

return (
  <div>
    {isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please log in.</h1>}
  </div>
);
```

---

### 🔄 Multiple Conditions with Switch Statement
Use this when there are **3 or more conditions** and readability matters.

```jsx
function StatusMessage({ status }) {
  switch (status) {
    case "loading":
      return <p>Loading...</p>;
    case "success":
      return <p>Data loaded successfully!</p>;
    case "error":
      return <p>There was an error loading the data.</p>;
    default:
      return <p>Unknown status.</p>;
  }
}
```

```jsx
<StatusMessage status="success" />
```

---

### ⚠️ Potential Pitfall with `&&`
```jsx
{unreadMessages.length && <h1>You have messages</h1>}
```
If `unreadMessages.length` is `0`, it returns `0` instead of rendering nothing. So:
- You might see a stray `0` in the DOM!
- Safer to use a strict condition like:
```jsx
{unreadMessages.length > 0 && <h1>...</h1>}
```

---

### 📋 Quiz Recap

**1. What is "conditional rendering"?**
> Displaying something **only when** a condition is met

**2. When would you use `&&`?**
> When you want to display something **or not display** anything

**3. When would you use a ternary?**
> When choosing between **two** outputs (if/else)

**4. What about more than 2 options?**
> Use `if...else if...else`, or a `switch` statement


---
## References