
2025-06-29 10:46

Status:

Tags: [React](3%20-%20Tags/React.md)

---
# React State - Scrimba

## 🧠 What is "State" in React?

> **State** is an object that holds **dynamic data** for a component — data that can **change over time** and cause the UI to re-render when it changes.

---

## ✅ Why Do We Need State?

Because **not everything in a UI is static**. We need state to:

---

### 1. **Track dynamic data in a component**

Examples:

- A counter that increases
    
- A form that captures user input
    
- A button that toggles a dropdown
    

```jsx
const [count, setCount] = useState(0);
```

✅ Without state, you'd have no way to **update or react to changes**.

---

### 2. **Control what the UI shows based on changes**

React uses **state changes to re-render** only what's needed.

```jsx
{isLoggedIn ? <Logout /> : <Login />}
```

✅ This is dynamic — React shows different content based on the state value.

---

### 3. **Store values between re-renders**

If you just use variables like this:

```jsx
let count = 0;
```

They’ll reset on every render. But `useState` **remembers values across renders**.

---

### 4. **User interaction = state changes**

- Typing into inputs = controlled components (`useState`)
    
- Clicking a button = changes state (`onClick`)
    
- Navigating pages = update current state
    

```jsx
<input value={name} onChange={e => setName(e.target.value)} />
```

---

## ✅ Summary Table

| Without State                | With State (`useState`)         |
| ---------------------------- | ------------------------------- |
| UI is static                 | UI can change                   |
| No reactivity                | Re-renders on state change      |
| No user interaction handling | Handles forms, toggles, updates |
| Can't track changes          | Tracks values over time         |

---

## 🧠 Metaphor:

Think of **state** as a component's **memory**.  
It lets React remember stuff — like button clicks, text input, or which tab you're on.

---

Let’s walk through **3 hands-on examples** of using **state** in React:

---

## ✅ Example 1: **Counter (Basic State)**

### 🧠 What it shows:

- Initialize state
    
- Update it on button click
    

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => setCount(count + 1)}>+ Increment</button>
      <button onClick={() => setCount(count - 1)}>- Decrement</button>
    </div>
  );
}
```

---

## ✅ Example 2: **Controlled Input (Forms + State)**

### 🧠 What it shows:

- Capture user input
    
- Reflect it in the UI
    

```jsx
import { useState } from 'react';

function NameInput() {
  const [name, setName] = useState('');

  return (
    <div>
      <label>Your name: </label>
      <input 
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <p>Hello, {name || "stranger"}!</p>
    </div>
  );
}
```

---

## ✅ Example 3: **Toggle UI (Conditional Rendering)**

### 🧠 What it shows:

- Toggling UI state (show/hide, login/logout, dark/light, etc.)
    

```jsx
import { useState } from 'react';

function ToggleMessage() {
  const [isVisible, setIsVisible] = useState(true);

  return (
    <div>
      <button onClick={() => setIsVisible(!isVisible)}>
        {isVisible ? 'Hide' : 'Show'} Message
      </button>

      {isVisible && <p>This message is visible!</p>}
    </div>
  );
}
```

---

## 🧠 Bonus: How It Works

| Action              | State Function             | Result                   |
| ------------------- | -------------------------- | ------------------------ |
| User types in input | `setName(e.target.value)`  | Updates text on screen   |
| Button click        | `setCount(count + 1)`      | Updates number on screen |
| Toggle click        | `setIsVisible(!isVisible)` | Shows/hides the element  |
|                     |                            |                          |

You have 2 options for what you can pass in to a state setter function (e.g. `setCount`). What are they?
	   - Pass the new version of state that we want to use as the
      replacement for the old version of state.

	   - Pass a callback function. Must return what we want the new
      value of state to be. Will receive the old version of state
      as a parameter so we can use it to help determine what we want
      the new value of state to be.

---
## References
[Props vs State - React](6%20-%20Main%20notes/Frontend/React/Props%20vs%20State%20-%20React.md)
[How react state controls UI - Re-render Cycle Explained](6%20-%20Main%20notes/Frontend/React/How%20react%20state%20controls%20UI%20-%20Re-render%20Cycle%20Explained.md)
[UseState - React](6%20-%20Main%20notes/Frontend/React/UseState%20-%20React.md)
[Thumb rule to Update state based on previous State - React](2%20-%20Source%20Material/FrontEnd%20Material/React/Thumb%20rule%20to%20Update%20state%20based%20on%20previous%20State%20-%20React.md)
[Lifting State up in React](6%20-%20Main%20notes/Frontend/React/Lifting%20State%20up%20in%20React.md)
[If you can avoid State, avoid State - React](6%20-%20Main%20notes/Frontend/React/If%20you%20can%20avoid%20State,%20avoid%20State%20-%20React.md)
[Event Listeners](6%20-%20Main%20notes/Frontend/Javascript%20notes/Event%20Listeners.md)
[Responding to Events - React](2%20-%20Source%20Material/FrontEnd%20Material/React/Responding%20to%20Events%20-%20React.md)
[Choosing state structure - React](6%20-%20Main%20notes/Frontend/React/Choosing%20state%20structure%20-%20React.md)
[Queueing a Series of State Updates - React](6%20-%20Main%20notes/Frontend/React/Queueing%20a%20Series%20of%20State%20Updates%20-%20React.md)
