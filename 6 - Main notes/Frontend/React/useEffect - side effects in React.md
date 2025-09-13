
2025-07-03 17:19

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

---
## 🧠 `useEffect` in React 
https://react.dev/reference/react/useEffect

### 🔍 Why Use `useEffect`?
React is excellent at handling UI updates, state, and props. However, React:
- **Cannot handle side effects on its own** (e.g., data fetching, direct DOM manipulation, subscriptions).

To manage these external interactions, React provides the `useEffect()` hook — **an escape hatch** to synchronize with external systems.

---

### ⚙️ What Are Side Effects?
Side effects are operations that:
- Affect things **outside the React component**
- Don’t directly relate to rendering UI

✅ **Examples of side effects**:
- Fetching API data
- Setting up subscriptions
- Reading/writing from `localStorage`
- Manually manipulating the DOM

🚫 **NOT side effects**:
- Updating state
- Rendering JSX
- Receiving props

---

### 📦 Basic Syntax
```jsx
useEffect(Setup function, depende, dependenciesArray)
```
- `setupFunction` — A function containing side-effect logic

- `dependenciesArray` — Tells React **when** to re-run the effect
	==If you omit this argument, your Effect will re-run after every re-render of the component.==

You need to pass two arguments to `useEffect`:

1. A _setup function_ with setup code that connects to that system.
    - It should return a _cleanup function_ with cleanup code that disconnects from that system.
2. A list of dependencies including every value from your component used inside of those functions.

**React calls your setup and cleanup functions whenever it’s necessary, which may happen multiple times:**

1. Your setup code runs when your component is added to the page _(mounts)_.
2. After every re-render of your component where the dependencies have changed:
    - First, your cleanup code runs with the old props and state.
    - Then, your setup code runs with the new props and state.
3. Your cleanup code runs one final time after your component is removed from the page _(unmounts)._
#### Returns [](https://react.dev/reference/react/useEffect#returns%20"Link%20for%20Returns")

`useEffect` returns `undefined`

---
#### Caveats [](https://react.dev/reference/react/useEffect#caveats%20"Link%20for%20Caveats")

- `useEffect` is a Hook, so you can only call it **at the top level of your component** or your own Hooks. You can’t call it inside loops or conditions. If you need that, extract a new component and move the state into it.
    
- If you’re **not trying to synchronize with some external system,** [you probably don’t need an Effect.](https://react.dev/learn/you-might-not-need-an-effect)
    
- When Strict Mode is on, React will **run one extra development-only setup+cleanup cycle** before the first real setup. This is a stress-test that ensures that your cleanup logic “mirrors” your setup logic and that it stops or undoes whatever the setup is doing. If this causes a problem, [](https://react.dev/learn/synchronizing-with-effects#how-to-handle-the-effect-firing-twice-in-development)
    
- If some of your dependencies are objects or functions defined inside the component, there is a risk that they will **cause the Effect to re-run more often than needed.** To fix this, remove unnecessary [](https://react.dev/reference/react/useEffect#removing-unnecessary-object-dependencies) and [](https://react.dev/reference/react/useEffect#removing-unnecessary-function-dependencies) dependencies. You can also [](https://react.dev/reference/react/useEffect#updating-state-based-on-previous-state-from-an-effect) and [](https://react.dev/reference/react/useEffect#reading-the-latest-props-and-state-from-an-effect) outside of your Effect.
    
- If your Effect wasn’t caused by an interaction (like a click), React will generally let the browser **paint the updated screen first before running your Effect.** If your Effect is doing something visual (for example, positioning a tooltip), and the delay is noticeable (for example, it flickers), replace `useEffect` with [`useLayoutEffect`.](https://react.dev/reference/react/useLayoutEffect)
    
- If your Effect is caused by an interaction (like a click), **React may run your Effect before the browser paints the updated screen**. This ensures that the result of the Effect can be observed by the event system. Usually, this works as expected. However, if you must defer the work until after paint, such as an `alert()`, you can use `setTimeout`. See [reactwg/react-18/128](https://github.com/reactwg/react-18/discussions/128) for more information.
    
- Even if your Effect was caused by an interaction (like a click), **React may allow the browser to repaint the screen before processing the state updates inside your Effect.** Usually, this works as expected. However, if you must block the browser from repainting the screen, you need to replace `useEffect` with [`useLayoutEffect`.](https://react.dev/reference/react/useLayoutEffect)
    
- Effects **only run on the client.** They don’t run during server rendering.


---
### 🕹️ Example – Fetching API Data
#### ❌ Bad Version (Runs Infinitely)
```jsx
export default function App() {
  const [starWarsData, setStarWarsData] = React.useState(null);

  // ❌ This runs on every render causing infinite fetch calls
  fetch("https://swapi.dev/api/people/1")
    .then(res => res.json())
    .then(data => setStarWarsData(data));

  return <pre>{JSON.stringify(starWarsData, null, 2)}</pre>;
}
```

#### ✅ Correct Version with `useEffect()`
```jsx
import React from "react";

export default function App() {
  const [starWarsData, setStarWarsData] = React.useState(null);

  React.useEffect(() => {
    fetch("https://swapi.dev/api/people/1")
      .then(res => res.json())
      .then(data => setStarWarsData(data));
  }, []); // Runs only once after first render

  return <pre>{JSON.stringify(starWarsData, null, 2)}</pre>;
}
```

---

### 🧮 Dependencies Array Explained
- `[]` → Run effect only **once** (on mount)
- `[stateVar]` → Run **when stateVar changes**
- Omit it → Run effect **after every render**

> 📌 React compares previous and current values in the dependencies array to decide whether to re-run the effect.

---

### 🔐 Why You Can’t Make `useEffect` Directly `async`
- `useEffect` expects **synchronous** cleanup behavior
- Making the function `async` returns a **Promise**, which breaks that pattern

✅ Solution:
```jsx
useEffect(() => {
  async function fetchData() {
    const res = await fetch(...);
    const data = await res.json();
    setData(data);
  }
  fetchData();
}, []);
```

---

### 🧰 useRef vs useState
#### `useRef()`
- Stores **mutable** values that **don’t trigger re-renders**
- Use it like a hidden pocket: `ref.current`
- Great for things like:
  - DOM elements
  - Timeout IDs
  - Persisting values between renders without updating the UI

#### `useState()`
- Stores state **that triggers re-render** when changed
- Meant for **render-relevant** values (e.g., form input, API data)

---

### 🚀 React’s Core Responsibilities
React handles:
- Rendering UI
- Managing local state
- Updating UI on state/prop changes

React **does NOT handle**:
- Fetching from external APIs
- Subscribing to events
- DOM measurements
- Working with 3rd-party libraries outside React

That’s where `useEffect()` comes in: a **safe zone** to synchronize side effects.

---
##  Usage
The `useEffect` Hook in React allows you to synchronize a component with an external system. Here's a summary of its usage:

- **Connecting to an External System**:
    
    - `useEffect` is used when a component needs to stay connected to external systems like the network, browser APIs, or third-party libraries while displayed on the page.
    - You call `useEffect` at the top level of your component.
    - It requires two arguments: a **setup function** that connects to the system and optionally returns a **cleanup function** to disconnect, and a **list of dependencies** that includes all reactive values used inside the setup and cleanup functions.
    - React calls your setup and cleanup functions multiple times as needed:
        - The setup code runs when the component **mounts** (is added to the page).
        - After every re-render where the dependencies have changed, the cleanup code runs with the old values, followed by the setup function with the new values.
        - The cleanup code runs one final time when the component **unmounts** (is removed from the page).
    - For example, if `serverUrl` or `roomId` change for a chat room component, the Effect will disconnect from the previous room and connect to the new one.
    - In **development mode**, React runs an extra `setup` and `cleanup` cycle before the first real setup to stress-test your Effect's logic and ensure cleanup is correctly implemented.
    - External systems include timers (`setInterval`, `clearInterval`), event subscriptions (`addEventListener`, `removeEventListener`), and third-party animation libraries. If not connecting to an external system, an Effect is likely not needed.
- **Wrapping Effects in Custom Hooks**:
    
    - Effects can be considered an "escape hatch" for stepping outside React's declarative paradigm.
    - To promote reusability and a more declarative API, you can **extract Effect logic into custom Hooks** (e.g., `useChatRoom`).
- **Controlling a Non-React Widget**:
    
    - `useEffect` can keep an **external, non-React widget synchronized** with your component's props or state.
    - For instance, it can call methods on a third-party map widget or video player to match its state to the React component's current state.
    - A cleanup function might not be necessary if the external widget manages only a DOM node that will be garbage-collected when the React component is removed.
- **Fetching Data with Effects**:
    
    - Effects can be used to **fetch data** for your component.
    - When fetching data, it's crucial to use a `cleanup` function (e.g., with an `ignore` variable) to prevent "race conditions" where network responses arrive out of order.
    - Directly fetching data in Effects can lead to issues like **not running on the server** (resulting in loading states initially), **network waterfalls**, and **lack of data preloading or caching**.
    - It is generally recommended to use your **framework's built-in data fetching mechanism** or **client-side caching libraries** (like React Query, useSWR, React Router 6.4+) instead of manual Effect-based data fetching.
- **Specifying Reactive Dependencies**:
    
    - **Every reactive value** (props, state, variables, and functions declared directly inside your component) used within an Effect's code **must be declared as a dependency**.
    - Omitting dependencies will trigger linter warnings.
    - To remove a dependency, you must ensure the value is no longer reactive (e.g., by moving it outside the component so it doesn't change on re-renders).
    - An Effect with an **empty dependency array (`[]`)** will only run once after the initial render and will not re-run when component props or state change.
    - **Never suppress the linter** for dependency warnings, as this can introduce bugs by "lying" to React about dependencies.
- **Updating State Based on Previous State from an Effect**:
    
    - If an Effect updates state based on its previous value (e.g., `setCount(count + 1)`), adding that state as a dependency will cause the Effect to re-run and reset.
    - To avoid this, use a **state updater function** (e.g., `setCount(c => c + 1)`). This allows the Effect to no longer depend on the state variable, preventing unnecessary re-runs.
- **Removing Unnecessary Object and Function Dependencies**:
    
    - If an Effect depends on an **object or function created during rendering**, it might re-run too often because these are new on every render.
    - To fix this, **create the object or declare the function _inside_ the Effect itself**. This ensures the Effect only depends on the primitive values (like strings or numbers) that the object/function relies on, preventing frequent re-runs.
- **Reading the Latest Props and State from an Effect (Experimental)**:
    
    - This section describes an **experimental API (`useEffectEvent`)** that is not yet released in a stable version of React.
    - It allows reading the _latest_ props and state from an Effect **without "reacting" to them**.
    - By declaring an `Effect Event` with `useEffectEvent` and moving non-reactive code inside it, you can omit the `Effect Event` from the Effect's dependencies, ensuring certain state changes don't re-run the Effect.
- **Displaying Different Content on the Server and the Client**:
    
    - Since Effects **only run on the client** and not during server rendering, you can use a state variable (e.g., `didMount`) initialized to `false` and set to `true` in an `useEffect` with an empty dependency array (`[]`).
    - This allows you to **conditionally render client-only JSX** once the component has mounted and hydrated on the client side.
    - This pattern should be used sparingly to avoid jarring changes for users on slow connections.

---
## ✅ useEffect Quiz Recap

1. **What makes React components like pure functions?**
   - Given same props/state → same rendered UI, no side effects

2. **What counts as a side effect?**
   - Anything React doesn’t control: API, localStorage, sockets

3. **What is NOT a side effect?**
   - Updating React state
   - Rendering JSX

4. **When does useEffect run?**
   - After mount
   - After every render (if no dependencies array)
   - When dependencies **change**

5. **What’s the purpose of the dependencies array?**
   - Tells React **when** to re-run the effect




---
## References
[You might not need an Effect - React](../../../2%20-%20Source%20Material/FrontEnd%20Material/React/You%20might%20not%20need%20an%20Effect%20-%20React.md)