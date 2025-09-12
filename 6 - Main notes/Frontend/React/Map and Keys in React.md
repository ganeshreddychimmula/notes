
2025-06-27 20:06

Status:

Tags: [JavaScript](../../../3%20-%20Tags/JavaScript.md)

---
# Map and Keys in React
It’s one of the most powerful tools for rendering lists dynamically from arrays.

---

## 🔁 What is `.map()`?

`.map()` is a **JavaScript array method** that transforms each item in an array into something new — in React, we use it to generate **JSX elements**.

---

## ✅ Basic Example

### Data:

```jsx
const fruits = ['Apple', 'Banana', 'Cherry'];
```

### JSX with `.map()`:

```jsx
<ul>
  {fruits.map(fruit => <li key={fruit}>{fruit}</li>)}
</ul>
```

> ✅ This will render:

```html
<ul>
  <li>Apple</li>
  <li>Banana</li>
  <li>Cherry</li>
</ul>
```

---

## 🔑 Why use a `key` in `.map()`?

React needs `key` to efficiently update or reorder items.  
It should be:

- ✅ Unique
    
- ✅ Consistent
    
- ❌ Not array index (unless you have no better option)
    

```jsx
items.map(item => <div key={item.id}>{item.name}</div>)
```

---

## 🧱 Real-World Component Example

```jsx
function UserList({ users }) {
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>
          {user.name} ({user.email})
        </li>
      ))}
    </ul>
  );
}
```

### Usage:

```jsx
<UserList users={[
  { id: 1, name: "Alice", email: "a@mail.com" },
  { id: 2, name: "Bob", email: "b@mail.com" }
]} />
```

---

## 🧠 TL;DR

|Feature|Description|
|---|---|
|What|Turns array into elements|
|Why|Dynamic rendering in loops|
|Needs `key`?|✅ Yes — always use a unique `key` prop|
|Can return|JSX, strings, components — anything renderable|

---

Let me know if you want me to update your canvas with a `.map()` example!
---
## References
[Keys property - React](Keys%20property%20-%20React.md)