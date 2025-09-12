
2025-08-18 09:54

Status:

Tags: [[../../../3 - Tags/React]]

---
# Render props - React
https://legacy.reactjs.org/docs/render-props.html

## 🧠 What is a Render Prop?

A **render prop** is a React pattern where a component accepts a **function as a prop**. This function returns a React element and gives control over rendering to the consumer of the component.

> The term "render prop" refers to a technique for sharing code between components using a prop whose value is a function.

---

## ✅ Why Use Render Props?

Render props provide a **flexible way to reuse component logic**, especially when:

- You need to share behavior without tightly coupling UI
    
- Higher-order components (HOCs) are too rigid or verbose

---

## 🔧 Basic Example

```jsx
function MouseTracker({ render }) {
  const [position, setPosition] = React.useState({ x: 0, y: 0 });

  function handleMouseMove(event) {
    setPosition({ x: event.clientX, y: event.clientY });
  }

  return (
    <div onMouseMove={handleMouseMove} style={{ height: '100vh' }}>
      {render(position)}
    </div>
  );
}

function App() {
  return (
    <MouseTracker render={({ x, y }) => (
      <h1>The mouse position is ({x}, {y})</h1>
    )} />
  );
}
```

### Key Points:

- `MouseTracker` handles logic (mouse tracking).
    
- The `render` prop lets the parent decide **how to display the data**.

---

## ✨ Benefits

|Benefit|Description|
|---|---|
|✅ Reusable Logic|Separate behavior from rendering|
|✅ UI Flexibility|Consumers control rendering completely|
|✅ Composable|Works well with functional composition|

---

## 📦 Alternative Syntax (Children as a Function)

Many render prop components accept `children` as a function instead of a named `render` prop.

```jsx
<MouseTracker>
  {({ x, y }) => <p>Mouse is at ({x}, {y})</p>}
</MouseTracker>
```

This is known as the **function-as-children** pattern.

---
## 🎯 Use Cases for Render Props

| Use Case                     | Description                                                                    |
| ---------------------------- | ------------------------------------------------------------------------------ |
| **Mouse Tracking**           | Track cursor position and let any component decide how to render that info     |
| **Form Handling**            | Share validation, input handling, and submit logic without enforcing UI        |
| **Toggling State**           | Abstract `on/off` logic while letting consumers render buttons, switches, etc. |
| **Animation State**          | Provide animation progress/timing data to custom-rendered components           |
| **Scroll Position Tracking** | Expose scroll positions for dynamic layouts or infinite scrolling              |
| **Online/Offline Detection** | Show different UIs based on network connectivity                               |
| **Window Resize Tracking**   | Adjust layout or behavior based on screen size                                 |
| **Drag-and-Drop Logic**      | Handle drag behavior while giving consumers full UI control                    |

### 🧠 Why Use Render Props in These Cases?

These use cases involve:

- **Behavior/state logic** that needs to be reused
    
- **Highly customized UI**, where HOCs or pre-built components would be too rigid
    

---

## 🧩 Related Concepts

### 1. **Higher-Order Components (HOC)**

HOCs are another way to reuse logic by wrapping components:

```jsx
const withTracking = (Component) => (props) => {
  const [x, setX] = useState(0);
  // ... tracking logic
  return <Component x={x} {...props} />
}
```

#### ❗ Downsides Compared to Render Props:

- Can lead to **prop clashing**
    
- Harder to **debug**
    
- Often harder to compose
    

### 2. **Custom Hooks** (Modern alternative)

```jsx
function useMousePosition() {
  const [pos, setPos] = useState({ x: 0, y: 0 });
  useEffect(() => {
    function handleMove(e) {
      setPos({ x: e.clientX, y: e.clientY });
    }
    window.addEventListener("mousemove", handleMove);
    return () => window.removeEventListener("mousemove", handleMove);
  }, []);
  return pos;
}

function Component() {
  const { x, y } = useMousePosition();
  return <p>Mouse at ({x}, {y})</p>;
}
```

✅ **Hooks** are now the preferred pattern for reusable logic in modern React (since v16.8), offering a cleaner and more readable syntax.

---

## 🔍 When to Use Render Props

| Use Case                                 | Render Props?  |
| ---------------------------------------- | -------------- |
| Share non-visual logic across components | ✅ Yes          |
| Customizing deeply nested UIs            | ✅ Yes          |
| Simplifying component logic with hooks   | ❌ Prefer Hooks |

---

## 🧾 Summary

- **Render props** let you write flexible, reusable components by passing a function that determines how they’re rendered.
    
- Best for sharing logic without dictating UI.
    
- Superseded in many use cases by **custom hooks**, but still useful in certain component-based designs.
    




---
## References