
2025-06-27 12:21

Status:

Tags: [[../../../3 - Tags/React]]

---
# Props - React

## 🧠 What are Props in React?

**Props** (short for **properties**) are how **data is passed** from one component to another — typically from **parent to child**.

They allow components to be **dynamic and reusable**.

There can be an arbitrary number of props and their values can be "hard-coded" strings or the results of JavaScript expressions. If the value of the prop is achieved using JavaScript it must be wrapped with curly braces.

---

## 🔧 Basic Syntax

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

function App() {
  return <Welcome name="Prashanth" />;
}
```

✅ `props.name` = `"Prashanth"`  
✅ `Welcome` is reusable with different `name` values.

---

> Note: ==The **parameter name** in a React component **does not have to be** `props`. It’s just a common convention.==

### 🔄 Same Function, Different Name (Still Works!)
```jsx
function Greeting(data) {   return <h1>Hello, {data.name}!</h1>; }
```

```jsx
function Greeting(xyz) {   return <h1>Hello, {xyz.name}!</h1>; }
```


> ✅ It works because whatever name you use is just the **name of the argument** holding the props object.


---

## 🧩 Why Props Matter

| Feature       | Benefit                                    |
| ------------- | ------------------------------------------ |
| Reusability   | Build once, use with different data        |
| Flexibility   | Customize behavior/UI with incoming values |
| Communication | Pass data between components cleanly       |

---

## 🧱 Props in Practice

### 🧑‍🎨 Function Component Example

```jsx
function Card({ title, content }) {
  return (
    <div className="card">
      <h3>{title}</h3>
      <p>{content}</p>
    </div>
  );
}

function App() {
  return (
    <>
      <Card title="React Props" content="Props let you pass data." />
      <Card title="React State" content="State lets components manage data." />
    </>
  );
}
```

---

## 🛠 How Props Are Used

### ✅ Destructuring in function parameter:

```jsx
function Profile({ name, age }) {
  return <p>{name} is {age} years old.</p>;
}
```

### ✅ Passing variables as props:

```jsx
const user = { name: "Alice", age: 25 };
<Profile name={user.name} age={user.age} />
```

### ✅ Conditional rendering via props:

```jsx
function Button({ disabled }) {
  return <button disabled={disabled}>Click Me</button>;
}
```

---

## ⚠️ Important Notes

- **Props are read-only** – you can’t change them inside the child component.
    
- To manage internal data, use **state** (`useState()`).
    

---

## 🧠 TL;DR

| Concept | Description                          |
| ------- | ------------------------------------ |
| Props   | Data passed from parent to child     |
| Syntax  | `<Component propName="value" />`     |
| Usage   | Customize behavior or render content |
| Rule    | Props are immutable inside child     |
E.g:

![[Pasted image 20250627143634.png]]
 

---
## References
[[Why enclose props in flower brackets in JSX or in React]]
[[Passing and Receiving Props - React]]
[[Question - Can I pass a custom Prop to a Native DOM Element ]]
[[Destructuring Concept]]
[[Handling Static assets(Like images) in React]]
[[Keys property - React]]
[[Some instances where props.children is useful - React]]