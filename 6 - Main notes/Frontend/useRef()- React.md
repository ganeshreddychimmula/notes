
2025-08-18 00:18

Status:

Tags: [[React]]

---
# React `useRef()` - Deep Dive and Related Concepts
https://react.dev/reference/react/useRef#manipulating-the-dom-with-a-ref

## 🧠 What is `useRef()`?

`useRef()` is a built-in React Hook that returns a **mutable object** with a `.current` property. It is used for two main purposes:

1. **Accessing DOM elements** directly (like in vanilla JavaScript).
    
2. **Storing mutable values** that persist across renders without causing re-renders.
    

```js
const myRef = useRef(initialValue)
```

- Returns an object: `{ current: initialValue }`
    
- Updating `myRef.current` **does NOT trigger a re-render**.

#### Parameters [](https://react.dev/reference/react/useRef#parameters "Link for Parameters")

- `initialValue`: The value you want the ref object’s `current` property to be initially. It can be a value of any type. This argument is ignored after the initial render.

#### Returns [](https://react.dev/reference/react/useRef#returns "Link for Returns")

`useRef` returns an object with a single property:

- `current`: Initially, it’s set to the `initialValue` you have passed. You can later set it to something else. **If you pass the ref object to React as a `ref` attribute to a JSX node, React will set its `current` property.** On the next renders, `useRef` will return the same object.

---

## ✅ Common Use Cases

### 1. **Accessing DOM Nodes**

```js
const inputRef = React.useRef(null)

useEffect(() => {
  inputRef.current.focus() // Focuses the input on mount
}, [])

return <input ref={inputRef} />
```

- `ref={inputRef}` attaches the `inputRef` to the actual DOM node.
    
- This is ==React’s alternative to `document.getElementById()`==.
    

### 2. **Persisting Values Across Renders (Without Causing Re-renders)**

```js
const renderCount = useRef(0)
renderCount.current++
console.log("Render Count:", renderCount.current)
```

- `renderCount` retains its value across re-renders.
    
- Modifying it **does not trigger another render**, unlike `useState()`.

### 3. **Storing Previous Props or State**

```js
const prevCount = useRef(count)

useEffect(() => {
  prevCount.current = count
}, [count])
```

- Useful for comparing previous and current values.

### 4. **Timers and Intervals**

```js
const timerRef = useRef(null)

useEffect(() => {
  timerRef.current = setInterval(() => console.log("tick"), 1000)
  return () => clearInterval(timerRef.current)
}, [])
```

---

## 🔬 How is `useRef` Different from `useState`?

| Feature            | `useRef`                 | `useState`       |
| ------------------ | ------------------------ | ---------------- |
| Triggers Re-render | ❌ No                     | ✅ Yes            |
| Mutable            | ✅ Yes (via `.current`)   | ✅ Yes            |
| DOM Access         | ✅ Common Use             | ❌ Not applicable |
| Best for           | Caching values, DOM refs | UI updates       |


---

## ⚠️ Important Notes

- `ref.current` is **not reactive**. Changes to it will not show up in the UI automatically.
    
- Do **not use refs to replace state** for values that affect what is displayed.
    
- * When dealing with **uncontrolled components** (like form inputs), refs are useful to read values without binding them to state.

### Caveats 
- You can mutate the `ref.current` property. Unlike state, it is mutable. However, if it holds an object that is used for rendering (for example, a piece of your state), then you shouldn’t mutate that object.
- When you change the `ref.current` property, React does not re-render your component. React is not aware of when you change it because a ref is a plain JavaScript object.
- Do not write _or read_ `ref.current` during rendering, except for [initialization.](https://react.dev/reference/react/useRef#avoiding-recreating-the-ref-contents) This makes your component’s behavior unpredictable. [^1]
	- Reading or writing `ref.current` inside the component's render body (outside `useEffect` or event handlers) can lead to **inconsistent behavior**, because React may call the render function multiple times. Use refs only for **storing values between renders**, not for reactive logic during render.
> 	✅ Safe: `const ref = useRef(0)`  
> 	❌ Risky: `if (ref.current === 0) { doSomething(); }` in render
- In Strict Mode, React will **call your component function twice** in order to [help you find accidental impurities.](https://react.dev/reference/react/useState#my-initializer-or-updater-function-runs-twice) This is development-only behavior and does not affect production. Each ref object will be created twice, but one of the versions will be discarded. If your component function is pure (as it should be), this should not affect the behavior.
	- In development mode, **React Strict Mode** calls your component function twice (mount → unmount → mount again) to detect side effects. This includes creating two versions of `ref` objects—only one is used. This does **not happen in production**, and **won’t cause issues if your component is pure**.
> 	⚠️ Impure code (e.g., modifying refs or state in render) may break under Strict Mode

---

## 🧩 Related Concepts

### 1. **Forwarding Refs**

Sometimes you want to pass a ref to a child component. For this, use `React.forwardRef()`.

```js
const MyInput = React.forwardRef((props, ref) => {
  return <input ref={ref} {...props} />
})
```

### 2. **`useImperativeHandle`**

Allows a parent to call specific methods on a child component’s ref.

```js
useImperativeHandle(ref, () => ({
  focus: () => inputRef.current.focus()
}))
```

Use with `forwardRef` for building custom, reusable input components.

### 3. **Class Component Equivalent**

In class components, refs are created using:

```js
this.inputRef = React.createRef()
```

---

## 🧠 When to Use `useRef()`

| Use Case                       | Use `useRef()`?       |
| ------------------------------ | --------------------- |
| Manual DOM manipulation        | ✅ Yes                 |
| Caching value across renders   | ✅ Yes                 |
| Want re-render on change       | ❌ No (use `useState`) |
| Trigger imperative methods     | ✅ Yes                 |
| Accessing previous state/props | ✅ Yes                 |

---

## ✅ Summary

- `useRef()` gives you a mutable container whose `.current` property can hold any value.
    
- It’s a powerful hook for **imperative logic**, DOM access, and **avoiding re-renders** for mutable values.
    
- Combine with `forwardRef` and `useImperativeHandle` for advanced custom component APIs.

---
## Example 
This example uses a combination of state and refs. Both `startTime` and `now` are state variables because they are used for rendering. But we also need to hold an [interval ID](https://developer.mozilla.org/en-US/docs/Web/API/setInterval) so that we can stop the interval on button press. Since the interval ID is not used for rendering, it’s appropriate to keep it in a ref, and manually update it.

```jsx
import { useState, useRef } from 'react';

export default function Stopwatch() {
  const [startTime, setStartTime] = useState(null);
  const [now, setNow] = useState(null);
  const intervalRef = useRef(null);

  function handleStart() {
    setStartTime(Date.now());
    setNow(Date.now());

    clearInterval(intervalRef.current);
    intervalRef.current = setInterval(() => {
      setNow(Date.now());
    }, 10);
  }

  function handleStop() {
    clearInterval(intervalRef.current);
  }

  let secondsPassed = 0;
  if (startTime != null && now != null) {
    secondsPassed = (now - startTime) / 1000;
  }

  return (
    <>
      <h1>Time passed: {secondsPassed.toFixed(3)}</h1>
      <button onClick={handleStart}>
        Start
      </button>
      <button onClick={handleStop}>
        Stop
      </button>
    </>
  );
}

```

### ⏱️ `Stopwatch` – Summary of Logic

```js
const intervalRef = useRef(null);
```

- Holds the `setInterval` ID.
    
- Doesn’t trigger re-renders when updated.

#### ▶️ `handleStart()`

1. Records start time (`setStartTime`) and current time (`setNow`).
    
2. Clears any previous interval.
    
3. Sets up a new interval that updates `now` every 10ms.

#### ⏹ `handleStop()`

- Clears the current interval using `intervalRef.current`.
    

#### 🧮 Time Calculation

```js
let secondsPassed = (now - startTime) / 1000;
```

- Only runs when both `startTime` and `now` are set.
    
- Displayed with 3 decimal places.
    

## ✅ Why `useRef()` is Used

- Stores the interval ID without causing re-renders.
    
- Allows clearing/replacing the interval on each “Start” or “Stop”.


---
## References
[^1]: [[Why not to read or write refs during rendering - React]]