
2025-06-27 19:50

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

---
# How React renders different types of Arrays
Let's explore **how React renders different types of arrays** when you just do:

```jsx
<div>{arr}</div>
```

The way React handles it depends on the **type of elements in the array**.

---

## 🧪 1. **Array of Strings or Numbers**

```jsx
const arr = ['React', 'is', 'fun'];
return <div>{arr}</div>;
```

✅ Output:

```html
<div>Reactisfun</div>
```

> React converts the array into a string using `arr.join('')`.

---

## 🧪 2. **Array of JSX Elements**

```jsx
const arr = [<p key="1">Hi</p>, <p key="2">There</p>];
return <div>{arr}</div>;
```

✅ Output:

```html
<div>
  <p>Hi</p>
  <p>There</p>
</div>
```

> ✅ This is the **preferred way** to render multiple components in JSX.  
> But remember to always add a **`key`** to each JSX element to avoid warnings.

---

## 🧪 3. **Array of Mixed Values**

```jsx
const arr = [<p key="1">Hi</p>, 'there', 42];
return <div>{arr}</div>;
```

✅ Output:

```html
<div>
  <p>Hi</p>
  there42
</div>
```

> ✅ React is smart enough to render JSX, strings, and numbers all together.  
> But it's **not recommended** to mix types — it can get messy.

---

## 🧪 4. **Array of Objects**

```jsx
const arr = [{ name: 'A' }, { name: 'B' }];
return <div>{arr}</div>;
```

❌ Output:

```html
<div>[object Object][object Object]</div>
```


> ❌ React renders object values as `[object Object]`  
> You must explicitly **map** and extract values:

```jsx
<div>
  {arr.map((item, i) => <p key={i}>{item.name}</p>)}
</div>
```

> Only JSX objects are rendered directly.
---

## 🧠 TL;DR: How React Renders Arrays in JSX

| Array Type      | Render Behavior                     | Notes                            |
| --------------- | ----------------------------------- | -------------------------------- |
| `['a', 'b']`    | `a,b`                               | `.join(',')` is applied          |
| `[<h1>Hi</h1>]` | JSX elements rendered normally      | ✅ Best practice                  |
| `[42, 'hello']` | Numbers and strings rendered inline | Allowed, but not super clean     |
| `[{}, {}]`      | `[object Object]` — not useful      | ❌ Map and render specific fields |

---
## References