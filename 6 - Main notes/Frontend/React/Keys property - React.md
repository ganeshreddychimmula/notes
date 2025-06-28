
2025-06-27 20:34

Status:

Tags:

---
# Key prop - React
The **`key` prop** in React is super important when rendering **lists with `.map()`** — it helps React track which items changed, were added, or removed.

---

## 🧠 What is the `key` Prop?

> A special prop you pass to **each list item** when rendering arrays.  
> It helps React **identify elements uniquely** across renders.

---

## ✅ Why `key` is needed

When React re-renders a list, it needs to know:

- Which item stayed the same
    
- Which item was removed
    
- Which one was added
    

| Without `key`, React may **re-render incorrectly** or **break animations or form inputs**.

---

## 🔧 Basic Example

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

✅ The `key={fruit}` ensures each `<li>` is uniquely identified.

---

## ❌ What happens without a `key`?

React will show a warning:

```
Each child in a list should have a unique "key" prop.
```

And React may not efficiently update the list.

---

## ⚠️ Using Array Index as Key: Be Careful

```jsx
{items.map((item, index) => <li key={index}>{item}</li>)}
```

✅ Works for static lists  
❌ Bad for dynamic lists (e.g. if you reorder, add, or remove items)

> 🔥 If you use index as key, and the array changes, React might mismatch the UI.

---

## ✅ Best Practices for `key`

|DO|DON'T|
|---|---|
|Use a **unique id** from your data|Use random values|
|Use `key={user.id}`|Use `key={index}` (only if necessary)|

---

## 🧠 Summary

|Feature|Value|
|---|---|
|Required?|✅ Yes for lists|
|Purpose|Uniquely identify elements|
|Good key|Stable, unique, predictable|


---
## References