
2025-06-27 19:38

Status:

Tags: 

---
# How React renders Arrays
**React can render arrays**, and it’s a common pattern — especially when displaying **lists of items** like cards, products, or user names.

---

## 🔁 Basic Example: Rendering an Array of Strings

```jsx
const fruits = ['Apple', 'Banana', 'Cherry'];

function FruitList() {
  return (
    <ul>
      {fruits.map(fruit => <li key={fruit}>{fruit}</li>)}
    </ul>
  );
}
```

> ✅ React renders each array element inside `<li>`, and `key` helps React track changes efficiently.

---

## 🧱 Rendering an Array of Components

```jsx
const users = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' }
];

function UserCard({ name }) {
  return <div>{name}</div>;
}

function UserList() {
  return (
    <>
      {users.map(user => <UserCard key={user.id} name={user.name} />)}
    </>
  );
}
```

---

## ⚠️ Important: Use a `key` prop

- Helps React identify each item uniquely
    
- Prevents unnecessary re-renders or rendering bugs
    

```jsx
{items.map(item => <div key={item.id}>{item.value}</div>)}
```

---

## ✅ TL;DR

|Question|Answer|
|---|---|
|Can React render arrays?|✅ Yes — with `map()` or loops|
|Common use case|Lists, cards, tables, repeated UI|
|Must use `key`?|✅ Yes — especially in `.map()` rendering|
|Can mix elements?|✅ Yes — arrays can include JSX, text, etc.|


---

## 📊 1. **Rendering an Array as a Table**

### Data:

```jsx
const users = [
  { id: 1, name: 'Alice', role: 'Admin' },
  { id: 2, name: 'Bob', role: 'User' },
  { id: 3, name: 'Charlie', role: 'User' },
];
```

### Table Component:

```jsx
function UserTable() {
  return (
    <table border="1">
      <thead>
        <tr>
          <th>ID</th><th>Name</th><th>Role</th>
        </tr>
      </thead>
      <tbody>
        {users.map(user => (
          <tr key={user.id}>
            <td>{user.id}</td>
            <td>{user.name}</td>
            <td>{user.role}</td>
          </tr>
        ))}
      </tbody>
    </table>
  );
}
```

> ✅ This renders each user as a table row using `.map()`.

---

## 🔍 2. **Rendering with Conditions (filter + map)**

Let’s say you only want to render **users with the role `User`**:

```jsx
function UserList() {
  return (
    <ul>
      {users
        .filter(user => user.role === 'User')
        .map(user => (
          <li key={user.id}>{user.name}</li>
        ))}
    </ul>
  );
}
```

> ✅ `.filter()` removes items you don’t want  
> ✅ `.map()` turns each item into JSX

---

## 🧠 Bonus: Combine `.filter()` and `.map()` in table

```jsx
function OnlyUsersTable() {
  return (
    <table border="1">
      <thead>
        <tr>
          <th>ID</th><th>Name</th>
        </tr>
      </thead>
      <tbody>
        {users
          .filter(user => user.role === 'User')
          .map(user => (
            <tr key={user.id}>
              <td>{user.id}</td>
              <td>{user.name}</td>
            </tr>
          ))}
      </tbody>
    </table>
  );
}
```

---

## ✅ Summary

|Feature|Code Example|
|---|---|
|Array to list|`items.map(item => <li>{item}</li>)`|
|Array to table rows|`users.map(user => <tr><td>...</td></tr>)`|
|Conditional render|`items.filter(...).map(...)`|

---
## References
[How React renders different types of Arrays](6%20-%20Main%20notes/Frontend/React/How%20React%20renders%20different%20types%20of%20Arrays.md)
[Map and Keys in React](6%20-%20Main%20notes/Frontend/React/Map%20and%20Keys%20in%20React.md)
[Keys property - React](6%20-%20Main%20notes/Frontend/React/Keys%20property%20-%20React.md)