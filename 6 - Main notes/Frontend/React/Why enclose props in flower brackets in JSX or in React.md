
2025-06-27 13:13

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

---
# Why enclose props in flower brackets in JSX or in React

## ❓ Why do we wrap props in `{}` inside JSX?

### ✅ Short Answer:

We use **curly braces `{}` in JSX** to embed **JavaScript expressions** — and `props` are JavaScript variables.

---

### 🔍 JSX is just JavaScript + XML-like syntax

JSX lets you **mix HTML-like syntax with JavaScript**, but:

- Anything inside JSX (like inside a `<div>`) that should be evaluated as JS **must go inside `{}`**.
    

### 🧠 Example:

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

✅ Here, `props.name` is a **JavaScript variable** — so we must use `{}` to tell JSX:

> “Evaluate this JavaScript expression.”

---

### 🚫 Wrong:

```jsx
<h1>Hello, props.name!</h1>  // ❌ This will print the literal text "props.name!"
```

---

## ✅ Other things you can embed in `{}`

```jsx
{2 + 2}           // numbers
{user.name}       // variables
{isLoggedIn && <LogoutButton />} // conditional logic
{items.map(...)} // loops```
```

---

Example :

```jsx
import ReactDOM from 'react-dom/client';

function App() {

  return (
    <h1>It is currently {new Date().getHours()}</h1>
  )
}

ReactDOM.createRoot(document.getElementById('root')).render(<App />);
```

---

## 🧠 Analogy:

Think of JSX as a template engine.  
>You use `{}` to **plug in dynamic data** — just like `{{ }}` in Handlebars or `${ }` in template literals.

---

## TL;DR

|Use Case|Do You Need `{}`?|Why?|
|---|---|---|
|Static text|❌ No|It's just HTML|
|Variables/props|✅ Yes|It’s JS, must be evaluated|
|Expressions|✅ Yes|Math, logic, function calls|

---
## References
[2 - JSX React](2%20-%20JSX%20React.md)