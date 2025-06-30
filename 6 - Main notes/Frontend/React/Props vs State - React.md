
2025-06-30 14:07

Status:

Tags:

---
# Props vs State - React
- Props refer to the properties that are being passed in to the component in order for it work correctly, similar to how a function receives a parameters: "from above". A component Receiving these components receiving props is not allowed to modify those props.(They are "immutable").
- Props are not meant to be changed.
- **State** refers to values that are managed by the component, similar to variables declared inside a function. 
- Anytime, you have values that keep changing ex: counter. That needs to be saved/displayed, you'll likely be using State.

Let’s compare **Props vs State** in React — two of the most important tools for managing data in your app.

## 🧠 Think of it like this:

- **Props** = External input (read-only)
    
- **State** = Internal memory (can change)
    
---

## 🧠 What’s the difference?

| Concept          | **Props**                        | **State**                                |
| ---------------- | -------------------------------- | ---------------------------------------- |
| **Definition**   | Data passed **into** a component | Data **managed by** the component itself |
| **Source**       | Parent component                 | Inside the component                     |
| **Mutability**   | **Read-only**                    | **Can change (via `useState`)**          |
| **Purpose**      | Share data across components     | Handle internal dynamic data             |
| **Updates UI?**  | ✅ Yes                            | ✅ Yes                                    |
| **Modified by?** | Parent                           | The component itself                     |

---

## ✅ Example: Using **Props**

```jsx
function Welcome({ name }) {
  return <h2>Hello, {name}!</h2>;
}

// Parent
<Welcome name="Alice" />
```

🧠 Here, `Welcome` receives `name` as a prop from the parent.

---

## ✅ Example: Using **State**

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </>
  );
}
```

🧠 Here, `count` is **state** managed inside the `Counter` component and updates on button click.

---

## 🔁 When to Use Each

| Scenario                             | Use                                |
| ------------------------------------ | ---------------------------------- |
| Displaying user data from parent     | **Props**                          |
| Capturing user input                 | **State**                          |
| Toggling a dropdown or modal         | **State**                          |
| Passing theme, language, or settings | **Props**                          |
| Sharing state between siblings       | **Lift state up → pass via Props** |

---

## 📦 Example: Combining Props + State

```jsx
function Message({ initialMessage }) {
  const [message, setMessage] = useState(initialMessage);

  return (
    <>
      <p>{message}</p>
      <button onClick={() => setMessage("Updated!")}>Change</button>
    </>
  );
}

// Parent
<Message initialMessage="Hello from parent!" />
```

---




---
## References
[[Props - React]]