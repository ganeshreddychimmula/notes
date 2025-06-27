
2025-06-27 15:25

Status:

Tags:

---
# Passing and Receiving Props - React

## 🔁 Overview: Props = Passing Data from Parent ➝ Child

Props are like **function parameters** for components.  
You **pass them** in the parent, and **receive them** in the child.

---

## ✅ 1. **Passing & Receiving a String Prop**

### 🔹 Parent Component

```jsx
function App() {
  return <Greeting name="Prashanth" />;
}
```

### 🔹 Child Component

```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// OR with destructuring
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}
```

---

## ✅ 2. **Passing Multiple Props (string, number)**

### 🔹 Parent

```jsx
<Product title="iPhone" price={999} />
```

### 🔹 Child

```jsx
function Product({ title, price }) {
  return (
    <div>
      <h2>{title}</h2>
      <p>Price: ${price}</p>
    </div>
  );
}
```

---

## ✅ 3. **Passing an Object Prop**

### 🔹 Parent

```jsx
<UserCard user={{ name: "Alice", age: 25 }} />
```

### 🔹 Child

```jsx
function UserCard({ user }) {
  return <p>{user.name} is {user.age} years old.</p>;
}
```

---

## ✅ 4. **Passing an Array Prop**

### 🔹 Parent

```jsx
<ItemsList items={["Apple", "Banana", "Cherry"]} />
```

### 🔹 Child

```jsx
function ItemsList({ items }) {
  return (
    <ul>
      {items.map((item, i) => (
        <li key={i}>{item}</li>
      ))}
    </ul>
  );
}
```

---

## ✅ 5. **Passing a Function as a Prop**

### 🔹 Parent

```jsx
function App() {
  const handleClick = () => alert("Button clicked!");
  return <ActionButton onClick={handleClick} />;
}
```

### 🔹 Child

```jsx
function ActionButton({ onClick }) {
  return <button onClick={onClick}>Click Me</button>;
}
```

---

## ✅ 6. **Passing JSX or Components via `children` Prop**

### 🔹 Parent

```jsx
<Card>
  <h2>This is inside the card!</h2>
</Card>
```

### 🔹 Child

```jsx
function Card({ children }) {
  return <div className="card">{children}</div>;
}
```

---

## 🧠 Summary Table

|Prop Type|Passed Like|Received As|
|---|---|---|
|String|`<Comp name="John" />`|`props.name` or `{ name }`|
|Number|`<Comp age={30} />`|`props.age` or `{ age }`|
|Object|`<Comp user={{name: "A"}} />`|`props.user.name`|
|Array|`<Comp items={[...]} />`|`props.items.map(...)`|
|Function|`<Comp onClick={fn} />`|`props.onClick()`|
|JSX/children|`<Comp>...</Comp>`|`props.children`|


---
## References