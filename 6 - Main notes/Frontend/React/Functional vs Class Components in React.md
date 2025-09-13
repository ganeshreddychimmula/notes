
2025-07-02 22:32

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

---
# Functional vs Class Components in React

The **class-based alternative** to functional programming in React is often referred to as the **“class component” model**, or **object-oriented style React components**.

Here’s a full comparison, focusing on how **class components** relate to the functional programming concepts we just discussed:

---

## 🏛️ Class-Based React Components (OOP-style)

Before hooks (pre-React 16.8), React used **class components** to manage state, lifecycle, and side effects. Although React now favors **functional components + hooks**, class components are still widely seen in older codebases.

---

## 🔄 Comparison to Functional Programming Concepts

|Functional Programming (Hooks)|Class-Based Alternative|
|---|---|
|`useState`|`this.state` + `this.setState()`|
|`useEffect`|Lifecycle methods like `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`|
|Pure functions|Class methods (often less pure, tied to instance)|
|Immutability (replace state)|Same – `this.setState()` merges shallowly|
|No side effects in render|Same rule – avoid side effects inside `render()`|

---

## 📦 Class Component Example (State + Event)

```jsx
import React from "react";

class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState(prevState => ({
      count: prevState.count + 1
    }));
  };

  render() {
    return (
      <div>
        <h1>Count: {this.state.count}</h1>
        <button onClick={this.increment}>+1</button>
      </div>
    );
  }
}
```

---

## 🔁 Lifecycle Methods (Class vs Functional)

| Purpose                    | Class Method             | Functional Alternative       |
| -------------------------- | ------------------------ | ---------------------------- |
| On mount (component loads) | `componentDidMount()`    | `useEffect(() => {}, [])`    |
| On update                  | `componentDidUpdate()`   | `useEffect(() => {})`        |
| On unmount                 | `componentWillUnmount()` | `useEffect(() => return...)` |

---

## ❓So is class-based React _not_ functional?

Not exactly:

- **Class components** are **OOP-based**, relying on **mutable instances**, `this`, and inheritance of lifecycle methods.
    
- **Functional components** use **functions**, **closures**, and **immutable patterns**, aligning more closely with **functional programming**.
    

---

## 🚦When to Use Class Components?

You’d use class components when:

- Working with legacy codebases
    
- Converting from older tutorials
    
- Learning how React evolved over time
    

But going forward, **React’s direction is functional** (hooks, Suspense, Server Components, etc.)

---

 **Meme Generator** example using a **class-based component** and Functional Components so you can compare both styles side-by-side.

---

## ✅ Functional Component (with Hooks)

```jsx
import { useState } from "react";

export default function MemeGenerator() {
  const [meme, setMeme] = useState({
    topText: "Something different",
    bottomText: "Walk into Mordor",
    imageUrl: "http://i.imgflip.com/1bij.jpg"
  });

  function handleChange(event) {
    const { name, value } = event.target;
    setMeme(prev => ({
      ...prev,
      [name]: value
    }));
  }

  return (
    <main>
      <div className="form">
        <label>Top Text
          <input
            type="text"
            name="topText"
            value={meme.topText}
            onChange={handleChange}
          />
        </label>

        <label>Bottom Text
          <input
            type="text"
            name="bottomText"
            value={meme.bottomText}
            onChange={handleChange}
          />
        </label>

        <button>Get a new meme image 🖼</button>
      </div>

      <div className="meme">
        <img src={meme.imageUrl} />
        <span className="top">{meme.topText}</span>
        <span className="bottom">{meme.bottomText}</span>
      </div>
    </main>
  );
}
```

---

## 🏛️ Class-Based Component (Same Functionality)

```jsx
import React from "react";

class MemeGenerator extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      meme: {
        topText: "Something different",
        bottomText: "Walk into Mordor",
        imageUrl: "http://i.imgflip.com/1bij.jpg"
      }
    };
  }

  handleChange = (event) => {
    const { name, value } = event.target;
    this.setState(prevState => ({
      meme: {
        ...prevState.meme,
        [name]: value
      }
    }));
  };

  render() {
    const { topText, bottomText, imageUrl } = this.state.meme;

    return (
      <main>
        <div className="form">
          <label>Top Text
            <input
              type="text"
              name="topText"
              value={topText}
              onChange={this.handleChange}
            />
          </label>

          <label>Bottom Text
            <input
              type="text"
              name="bottomText"
              value={bottomText}
              onChange={this.handleChange}
            />
          </label>

          <button>Get a new meme image 🖼</button>
        </div>

        <div className="meme">
          <img src={imageUrl} />
          <span className="top">{topText}</span>
          <span className="bottom">{bottomText}</span>
        </div>
      </main>
    );
  }
}

export default MemeGenerator;
```

---

## 🔍 Key Differences

|Concept|Functional (Hooks)|Class-Based|
|---|---|---|
|State|`useState()`|`this.state` in constructor|
|Update state|`setMeme({...})`|`this.setState({...})`|
|Event handlers|Inline functions or arrow functions|Must bind or use arrow functions|
|Rerender|Triggers automatically on state update|Same – via `this.setState()`|
|Scope|Closure + lexical scope|`this` keyword (must be careful!)|

---

![Pasted image 20250702191627](../../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250702191627.png)



---
## References