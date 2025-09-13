
2025-07-20 10:15

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

---
# Advanced React - scrimba
### 1. React Children [^1]

"React children" refers to whatever content is placed between the opening and closing tags of a React component1. This content can be anything: plain text, HTML elements, other React components, or even a mix of these. You can access this content inside the component via the

`props.children` property2.

JavaScript
```js
export default function Button (props) {
  return (
    <button {...props}>
      {props.children} 
    </button>
  )
}
```

In this
`Button` component, `{props.children}` 3 renders whatever is passed between the
`<Button>` and `</Button>` tags when it's used. For instance, if you write
`<Button>Click me</Button>`, then "Click me" becomes `props.children`4.

**How it relates:** The concept of `children` is fundamental to building flexible and reusable components. It allows components to "wrap" content, making them highly composable. This becomes particularly relevant when discussing "compound components" later, as `children` are essential for their structure.

### 2. Props Spreading

"Props spreading" is a concise way to pass all the properties from one object (often the`props` object received by a component) to another element or component using the spread syntax (`...`).

JavaScript
```js
export default function Button (props) {
  return (
    <button {...props}> [cite: 14]
      {props.children}
    </button>
  )
}
```

Here,
`{...props}` on the `<button>` element means that any prop passed to the `Button` component (e.g., `onClick`, `id`, `style`) will automatically be passed down to the native HTML `<button>` element.

**How it relates:** ==Props spreading is a powerful feature for creating flexible components that can accept and forward any standard HTML attributes or custom props==. It's often used in conjunction with "props destructuring" to manage props effectively.

### 3. Props Destructuring [^3]
Props destructuring is an ES6 feature that allows you to extract **specific** properties from the `props` object into their own named variables. This makes your component code cleaner and more readable, as you don't have to repeatedly type `props.` before each prop name. You can also use the rest operator (`...rest`) to gather any remaining props that weren't explicitly destructured.

**Example from the document:**

JavaScript

```js
export default function Button({children, ... rest}) { [cite: 20]
  console.log(rest) [cite: 21]
  return (
    <button>
      {children} [cite: 24]
    </button>
  )
}
```

In this example,

`children` is directly extracted, and all other props are collected into the `rest` object.

**How it relates:** Props destructuring is a common pattern for managing props, especially when dealing with a large number of them or when you want to explicitly name the props a component expects. It works very well with props spreading, as you can destructure specific props you want to handle, and then spread the

`...rest` props to the underlying element, avoiding issues like the "className prop overwritten problem".

### 4. ClassName Prop Overwritten Problem

This problem occurs when you try to apply a `className` based on internal logic (e.g., `sizeClass` ) and also allow an external `className` to be passed via props. If you simply apply both like `<button className={sizeClass} className={className}>`, the latter `className` would overwrite the former.

Solution (1st way):
You combine the internally generated sizeClass with the externally provided className using a template literal:

JavaScript
```js
export default function Button({children, className, size,... rest}) { [cite: 30]
  let sizeClass [cite: 35]
  if (size === "sm") sizeClass = "button-small" [cite: 36]
  if (size === "lg") sizeClass = "button-large" [cite: 37]
  return (
    <button className={` ${sizeClass} ${className} `} {... rest}> [cite: 38]
      {children} [cite: 39]
    </button>
  )
}
```
By combining them within a single `className` attribute, both classes are applied.

Solution (2nd way):
Using packages like
[clsx](https://www.npmjs.com/package/clsx) or [classnames](https://www.npmjs.com/package/classnames). 
These libraries are specifically designed to help construct `className` strings conditionally and elegantly, making it easier to manage multiple classes.

**How it relates:** This problem highlights the importance of careful prop management when using features like props spreading and destructuring. While spreading is convenient, you need to be aware of potential conflicts and how to resolve them, ensuring that all intended props are correctly applied.

### 5. Prop Drilling 

Prop drilling happens when a component deep down in the component tree needs access to data that originates from a grandparent (or higher) component, and this data is manually passed down through each intermediate child component until it reaches the component that actually needs it. 
![Pasted image 20250720191015](../../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250720191015.png)The above diagram illustrates this, showing "State" at the top and "Props" being passed down through many layers of components to a deeply nested one.
![Pasted image 20250720205846](../../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250720205846.png)


**Solutions to Prop Drilling:**

- **Do nothing:** For shallow component trees (1 or 2 levels deep), simply passing props down is often the simplest and most readable solution. Kent C. Dodds' "AHA Programming" (Avoid Hasty Abstractions) principle suggests not over-optimizing or introducing complex solutions for simple problems. https://kentcdodds.com/blog/aha-programming [^5]
    
- **Context API:** React's Context API provides a way to pass data through the component tree without manually passing props at every level. Components can access the state directly from a Context Provider, regardless of how deep they are in the tree.
    
- **State Management Libraries:** Libraries like Redux, Zustand, Recoil, etc., provide centralized state management, allowing any component to connect to the store and access the necessary state without props.
    
- **Compound Components:** This pattern is listed as a solution to prop drilling. It flattens the structure and allows easier passing of props to deeply nested components.
    
**How it relates:** Prop drilling is a problem that arises from a strictly hierarchical prop flow when state needs to be shared widely.

`props.children` (and the broader concept of component composition) is one way to naturally flatten the component structure, which relates to "compound components" as a solution to prop drilling.

### 6. Compound Components [^6]

- Compound components are a design pattern in React where **multiple components work together as a unit, sharing implicit state and logic**, to provide a single, cohesive user interface feature.
- They leverage`props.children` to compose their parts. The benefit is that they flatten the structure and make it easier to pass props to deeply-nested components. They also often have dedicated functions or styling 25and make the component structure more transparent.

**How it relates:** Compound components are a direct solution to managing complex component interactions and can alleviate prop drilling by allowing child components to implicitly access shared context or state provided by the parent compound component, rather than explicitly passing props through many layers. They heavily rely on the `children` prop to enable flexible composition.
![Pasted image 20250720205905](../../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250720205905.png)


### 7.   Implicit State
![Pasted image 20250720210403](../../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250720210403.png)
While the example _shows_ the structure, for `MenuButton` to actually _toggle_ the `MenuDropdown`'s visibility, the `Menu` component needs to share its `open` state and `toggle` function with its children. The two primary methods for this in Compound Components are:
- `React.Children` - API provided by React( not top be confused with props.children)
- `Context`

### 8. React.Children and React.cloneElement() [^8]
- Not usually the preferred way.
- Used to pass props to children
	- utility  that provides methods for interacting with component's direct children elements.
		- React.Children.map()
		- React.Children.forEach()
- We will use in conjunction with React.cloneElement()
	- Utility that duplicates a React element and provides a way to inject additional props to that element.
	- Essentially same as `Object.assign()` 
	- when we use with React.Children.map(), it can be used to "augment" the original children with new props.
- Shortcomings of React.children
	- Fragile - Children need to be designed keeping React.Children requirements in mind
	- You could not pass props deep.

### 9. React Context [^9]
- Solution for props drilling
- we are going to add a parent component?(provider) to entire application or as high as we need to
- Provider contains values we need.
- we use `useContext()` hook to access the values
-   How to Use:
```js
// create a context
const ThemeContext = React.createContext()
export default function App() {
    return (
    // wrap with theme provider
        <ThemeContext.Provider value="light">
            <div className="container dark-theme">
                <Header />
                <Button />
            </div>
        </ThemeContext.Provider>
    )
}
// Export the context.  
export { ThemeContext }
```
- `value`  will be accessible to everthing inside the provider.
```js
import {ThemeContext} from "./App"

export default function Button() {
    const value = React.useContext(ThemeContext)
    return (
        <button className={`${value}-theme`}>
            Switch Theme
        </button>
    )
}
```

- If we want to send multiple variables, then send it as an object with multiple keys
- 


### 10. Compound Components w/ dot syntax [^10]
```js
// src/components/index.js
import Menu from "./Menu"
import MenuButton from "./MenuButton"
import MenuDropdown from "./MenuDropdown"
import MenuItem from "./MenuItem"
  
Menu.Button = MenuButton
Menu.Dropdown = MenuDropdown
Menu.Item = MenuItem

export default Menu

// src/index.jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import Menu from "./Menu/index"
  
function App() {
  const sports = ["Tennis", "Pickleball", "Racquetball", "Squash"]
  
  return (
    <Menu>
      <Menu.Button>Sports</Menu.Button>
      <Menu.Dropdown>
        {sports.map(sport => (
          <Menu.Item key={sport}>{sport}</Menu.Item>
        ))}
      </Menu.Dropdown>
    </Menu>
  )
}
  
ReactDOM.createRoot(document.getElementById('root')).render(<App />);

```

### 11. Headless Components [^11]

- Headless components don't have any styled UI to display ;
- They're purely intended to provide functionality.
- Headless components are a **clean, reusable way** to share behavior (like toggle logic) across components without enforcing UI. By combining the **Context API**, **dot syntax**, and **composition**, you give consumers **full control** over rendering while centralizing logic in one place.
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
- You can directly include toggle in menu components

### 12. useRef() [^12]
- Refs are just like state, just changing them doesn't cause re-render. They are frequently used for manual DOM manipulation.
-  let renderCount = React.useRef(0)
	- here, renderCount is a object, with current property set to 0;
	- If you want to access renderCount, you need to use `renderCount.current`
- When you are trying to create a ref to access a DOM node, you intialize the ref with null.
	`const inputRef = React.useRef(null)`
- To assign the newly created ref to a React component, you use a property provided by Reaact itself - `ref`

### 13. Render Props [^13]
- A **render prop** is a React pattern where a component accepts a **function as a prop**. This function returns a React element and gives control over rendering to the consumer of the component.
- Passing a function as a prop to children, such that it can manipulate data in parent component by passing a bool value.
- Parent can make decisions based on internal state of the children. possible applications:
	- Can display or hide JSX based on the data received from children.
```js
// Decision.js
import React from "react"
export default function Decision({ render }) {
    const [goingOut, setGoingOut] = React.useState(false)
    function toggleGoingOut() {
        setGoingOut(prev => !prev)
    }
    return (
        <div>
            <button onClick={toggleGoingOut}>Change mind</button>
            {render(goingOut)}
        </div>
    )
}

// App.js
function App() {
    return (
        <div>
            <Decision render={(goingOut) => {
                return (
                    <h1>
                        Am I going out tonight?? {goingOut ?
                        "Yes!" : "Nope..."}
                    </h1>
                )
            }} />
        </div>
    )
}
```

### 14. Custom Hooks [^14]
- ![Pasted image 20250818130755](../../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250818130755.png)
- Combining Existing hooks into custom, reusable pieces of logic 
- Similar to regular utility functions, but use hooks to access the render cycles of React.
```jsx
```

---
## References
[^1]: [Some instances where props.children is useful - React](Some%20instances%20where%20props.children%20is%20useful%20-%20React.md)
[^3]: [props de-structuring and its importance - React](props%20de-structuring%20and%20its%20importance%20-%20React.md)
[^5]: [AHA Programming](../../../2%20-%20Source%20Material/Articles/AHA%20Programming.md)
[^6]: [Compound components - React](Compound%20components%20-%20React.md)
[^8]: [React.Children and React.cloneElement()](React.Children%20and%20React.cloneElement().md)
[^9]: [React Context](React%20Context.md)
[^10]: [Compound components with dot syntax - React](Compound%20components%20with%20dot%20syntax%20-%20React.md)
[^11]: [Headless Components - React](Headless%20Components%20-%20React.md)
[^12]: [useRef()- React](useRef()-%20React.md)
[^13]: [Render props - React](Render%20props%20-%20React.md)
[^14]: [Custom hooks - React](Custom%20hooks%20-%20React.md)
[React Router 6](React%20Router%206.md)