
2025-07-02 15:33

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

---
## 🎛️ State Sharing and Prop Passing in React – Explained

### 🔁 Passing State as Props

- When **props change**, a component may re-render — but:
  - It's a **partial truth**.
  - **All child components** of a parent **re-render** if the **parent re-renders**, unless they are Memoized.

### 🧭 State & Props: How They Work Together

- **State** is local to a component.
- **Props** allow **passing data down** from a parent component to its children.
- To **share state between sibling components**, you must:
  - Lift the shared state **up** to their **common parent**.

> 📌 This process is called ==**“lifting state up.”**==

### 📉 Visual Explanation
If A is the parent of B and C, and you want to pass state from B → C:
1. Lift B’s state to A.
2. Pass it down to both B and C via props.

```
A (holds state)
├── B (uses prop)
└── C (uses prop)
```

### 🧰 State Management Solutions
- For deeply nested components or global state:
  - **React Context API**
  - **Redux**, **Zustand**, or other third-party state managers

> Use **Context/Redux** when:
> - Many components need the same data
> - You want to avoid prop drilling (passing props through layers)

---

## 🟢 Local State Example
```jsx
import React from "react"

export default function Pad(props) {
  const [on, setOn] = React.useState(props.on);

  function toggle() {
    setOn(prevOn => !prevOn);
  }

  return (
    <button
      style={{ backgroundColor: props.color }}
      className={on ? "on" : undefined}
      onClick={toggle}
    ></button>
  );
}
```

> 🔍 Local to the `Pad` component — changes won’t affect other Pads.

---

## 🔄 Shared State (Controlled by Parent)

To coordinate multiple `Pad` components:
- Parent owns the state.
- Each child receives props + callback handler.

### 📦 Child Component
```jsx
import React from "react"

export default function Pad(props) {
  return (
    <button
      style={{ backgroundColor: props.color }}
      className={props.on ? "on" : undefined}
      onClick={() => props.toggle(props.id)}
    ></button>
  );
}
```

> ⛔ Note: `key` is a special prop used internally by React. You **cannot access it** from props in the component.

### 🧑‍🎓 Parent Component
```jsx
import React from "react"
import padsData from "./pads"
import Pad from "./Pad"

export default function App() {
  const [pads, setPads] = React.useState(padsData);

  function toggle(id) {
    setPads(prevPads =>
      prevPads.map(pad =>
        pad.id === id ? { ...pad, on: !pad.on } : pad
      )
    );
  }

  const buttonElements = pads.map(pad => (
    <Pad
      key={pad.id}
      id={pad.id}
      color={pad.color}
      on={pad.on}
      toggle={toggle}
    />
  ));

  return <main><div className="pad-container">{buttonElements}</div></main>;
}
```

> ✅ Now, when you click a Pad, it informs the parent to update its state.
> React then **re-renders** the affected components.



---
## References