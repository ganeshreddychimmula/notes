
2025-08-17 23:38

Status:

Tags:

---
# Headless Components - React
- Headless components don't have any styled UI to display ;
- They're purely intended to provide functionality.
### Example (Explanation at bottom)
```js
// sec/Toggle/Toggle.jsx
import React from "react"

const ToggleContext = React.createContext()

export default function Toggle({ children }) {
    const [on, setOn] = React.useState(false)
    function toggle() {
        setOn(prevOn => !prevOn)
    }
    return (
        <ToggleContext.Provider value={{ on, toggle }}>
            {children}
        </ToggleContext.Provider>
    )
}
export { ToggleContext }

// ToggleButton.jsx
import React from "react"
import { ToggleContext } from "./Toggle"

export default function ToggleButton({ children }) {
    const { toggle } = React.useContext(ToggleContext)
    return (
        <div onClick={toggle}>
            {children}
        </div>
    )
}

// ToggleOn.jsx
import React from "react"
import { ToggleContext } from "./Toggle"

export default function ToggleOn({ children }) {
    const { on } = React.useContext(ToggleContext)
    return !on ? null : children
}

// ToggleOff.jsx
import React from "react"
import { ToggleContext } from "./Toggle"

export default function ToggleOff({ children }) {
    const { on } = React.useContext(ToggleContext)
    return on ? null : children
}

// /src/Toggle/index.js - 
import Toggle from "./Toggle"
import ToggleButton from "./ToggleButton"
import ToggleOn from "./ToggleOn"
import ToggleOff from "./ToggleOff"

Toggle.Button = ToggleButton // DOT syntax
Toggle.On = ToggleOn
Toggle.Off = ToggleOff

export default Toggle
```


```js
// index.jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import Star from "./Star"
import Toggle from "./Toggle/index"
import { BsStar, BsStarFill } from "react-icons/bs"

function App() {
  return (
    <>
      <Toggle>
        <Toggle.Button>
          <Toggle.On>
            <BsStarFill className="star filled" />
          </Toggle.On>
          
          <Toggle.Off>
            <BsStar className="star" />
          </Toggle.Off>
        </Toggle.Button>
      </Toggle>
      
      <Toggle>
        <Menu>
          <Toggle.Button>
            <Menu.Button>Menu</Menu.Button>
          </Toggle.Button>
          <Toggle.On>
            <Menu.Dropdown>
              <Menu.Item>Home</Menu.Item>

              <Menu.Item>About</Menu.Item>

              <Menu.Item>Contact</Menu.Item>

              <Menu.Item>Blog</Menu.Item>
            </Menu.Dropdown>
          </Toggle.On>
        </Menu>
      </Toggle>
    </>
  )

}

  

ReactDOM.createRoot(document.getElementById('root')).render(<App />);
```
![Pasted image 20250723190149](../../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250723190149.png)
![Pasted image 20250723190203](../../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250723190203.png)
**FYI:** You can directly include toggle in menu components


# Headless Components in React - Explained with Example

## 🧠 What Are Headless Components?

**Headless components** in React are components that **do not render any UI of their own**. Instead, they provide **behavioral logic and state** to child components, which are responsible for defining the UI.

They are sometimes called ==**"logic-only components"**==, and are often used in:

- Design systems
    
- Reusable libraries
    
- Component abstractions (e.g., `react-table`, `downshift`, `@headlessui/react`)

> **Think of them as components that separate the logic from the presentation.**

---

## ✅ Why Use Headless Components?

|Benefit|Explanation|
|---|---|
|✅ Reusability|Reuse logic without enforcing a UI design|
|✅ Flexibility|Let consumers design their own UI|
|✅ Separation of Concerns|Keeps logic and rendering responsibilities separate|
|✅ Customization|Developers can compose any UI around the shared behavior|

---

## 🔧 Toggle Example (Headless Component)

We will build a headless `Toggle` component and its companion components: `Toggle.Button`, `Toggle.On`, and `Toggle.Off`.

### Folder Structure:

```
/src/Toggle/
  Toggle.jsx
  ToggleButton.jsx
  ToggleOn.jsx
  ToggleOff.jsx
  index.js
```

### 🔸 Toggle.jsx (Core Provider)

```js
import React from "react"

const ToggleContext = React.createContext()

export default function Toggle({ children }) {
  const [on, setOn] = React.useState(false)
  function toggle() {
    setOn(prevOn => !prevOn)
  }

  return (
    <ToggleContext.Provider value={{ on, toggle }}>
      {children}
    </ToggleContext.Provider>
  )
}

export { ToggleContext }
```

- This component **doesn't render any UI**.
    
- It provides `on` state and `toggle()` function via Context.

### 🔸 ToggleButton.jsx

```js
import React from "react"
import { ToggleContext } from "./Toggle"

export default function ToggleButton({ children }) {
  const { toggle } = React.useContext(ToggleContext)
  return <div onClick={toggle}>{children}</div>
}
```

### 🔸 ToggleOn.jsx

```js
import React from "react"
import { ToggleContext } from "./Toggle"

export default function ToggleOn({ children }) {
  const { on } = React.useContext(ToggleContext)
  return on ? children : null
}
```

### 🔸 ToggleOff.jsx

```js
import React from "react"
import { ToggleContext } from "./Toggle"

export default function ToggleOff({ children }) {
  const { on } = React.useContext(ToggleContext)
  return on ? null : children
}
```

### 🔸 index.js (Dot Syntax Setup)

```js
import Toggle from "./Toggle"
import ToggleButton from "./ToggleButton"
import ToggleOn from "./ToggleOn"
import ToggleOff from "./ToggleOff"

Toggle.Button = ToggleButton
Toggle.On = ToggleOn
Toggle.Off = ToggleOff

export default Toggle
```

---

## 🧪 Using the Toggle Component

```jsx
import Toggle from "./Toggle/index"
import { BsStar, BsStarFill } from "react-icons/bs"

function App() {
  return (
    <>
      <Toggle>
        <Toggle.Button>
          <Toggle.On>
            <BsStarFill className="star filled" />
          </Toggle.On>
          <Toggle.Off>
            <BsStar className="star" />
          </Toggle.Off>
        </Toggle.Button>
      </Toggle>
    </>
  )
}
```

### Behavior:

- Clicking the star toggles the state
    
- Only one of `Toggle.On` or `Toggle.Off` shows at a time
    
- **You can wrap any UI around this logic**

---

## 🧩 Extending Headless Behavior

You can use the same `Toggle` logic in many different ways:

- Show/hide a modal
    
- Toggle a dropdown menu
    
- Switch between dark/light themes
    
- Control animations

### Example with Menu:

```jsx
<Toggle>
  <Menu>
    <Toggle.Button>
      <Menu.Button>Menu</Menu.Button>
    </Toggle.Button>
    <Toggle.On>
      <Menu.Dropdown>
        <Menu.Item>Home</Menu.Item>
        <Menu.Item>About</Menu.Item>
      </Menu.Dropdown>
    </Toggle.On>
  </Menu>
</Toggle>
```

---

## 🧠 Key Concepts

- - **Compound Components**
    
- **Context API**: Enables communication between headless component and its consumers.
    
- **Dot Syntax**: Makes API intuitive and self-documenting.
    
- **Children as Functions** (Alternative): Another headless pattern is using render props instead of dot syntax.


---

## ✅ When to Use Headless Components

|Use Case|When|
|---|---|
|Design System|You want to expose functionality but leave UI to the consumer|
|Reusability|Shared state logic is used in multiple places|
|Library Building|You're building tools/components others will style|

---

## 🧾 Summary

Headless components are a **clean, reusable way** to share behavior (like toggle logic) across components without enforcing UI. By combining the **Context API**, **dot syntax**, and **composition**, you give consumers **full control** over rendering while centralizing logic in one place.

---

> You can use toggle inside the menu

```jsx
// Menu/ToggleMenu.jsx
import React from "react"
import Toggle from "../Toggle"

const MenuContext = React.createContext()

export default function Menu({ children }) {
  return (
    <Toggle>
      <MenuContext.Provider value={{}}>
        <div className="menu">{children}</div>
      </MenuContext.Provider>
    </Toggle>
  )
}

export { MenuContext }

```

## ✅ Benefits of Including `Toggle` Inside `Menu`

|Benefit|Description|
|---|---|
|🧼 Cleaner API|Consumers don't need to manage `Toggle` separately|
|📦 Better Encapsulation|Logic and UI live in a single reusable component|
|🔒 Less Error-Prone|Reduces risk of incorrect context nesting|
|⚙️ Still Reusable Internally|Can still use the same `Toggle` logic for other patterns|
If you're building a design system or UI component library, this pattern makes the API **developer-friendly** while keeping your logic **modular and composable**.
### 🔧 Example of Internal Toggle Use

```jsx
// Menu.jsx
import Toggle from "../Toggle"

export default function Menu({ children }) {
  return (
    <Toggle>
      <div className="menu">{children}</div>
    </Toggle>
  )
}

// Menu.Button.jsx
import { useContext } from "react"
import { ToggleContext } from "../Toggle"

export function MenuButton({ children }) {
  const { toggle } = useContext(ToggleContext)
  return <button onClick={toggle}>{children}</button>
}

// Menu.Dropdown.jsx
import { useContext } from "react"
import { ToggleContext } from "../Toggle"

export function MenuDropdown({ children }) {
  const { on } = useContext(ToggleContext)
  return on ? <ul>{children}</ul> : null
}

```
### ✅ After (Embedding `Toggle` inside `Menu`)

```jsx
<Menu>
  <Menu.Button>Menu</Menu.Button>
  <Menu.Dropdown>
    <Menu.Item>Home</Menu.Item>
    <Menu.Item>About</Menu.Item>
  </Menu.Dropdown>
</Menu>
```

- Internally, `Menu` uses the `Toggle` logic (via context).
    
- Consumer just uses `Menu` as a regular component without needing to know about `Toggle`.

---
## References