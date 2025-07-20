
2025-07-20 19:17

Status: [[React]]

Tags: 

---
# Compound components - React

- Compound components are a design pattern in React where **multiple components work together as a unit, sharing implicit state and logic**, to provide a single, cohesive user interface feature.
- They leverage`props.children` to compose their parts. The benefit is that they flatten the structure and make it easier to pass props to deeply-nested components. They also often have dedicated functions or styling and make the component structure more transparent.

```js
//Menu.jsx
export default function Menu({ children }) {
    const [open, setOpen] = React.useState(true)
    function toggle() {
        setOpen(prevOpen => !prevOpen)
    }
    return (
        <div className="menu">
            {children}
        </div>
    )
}

// MenuButton.jsx
export default function MenuButton({children, ...props }) {
    return (
        <Button {...props}>{children}</Button>
    )
}

// MenuItem.jsx
export default function MenuItem({ children }) {
    return (
        <div className="menu-item">
            {children}
        </div>
    )
}

// use
function App() {
  const sports = ["Tennis", "Pickleball", "Racquetball", "Squash"]
  return (
    <Menu>
      <MenuButton>Sports</MenuButton>
      <MenuDropdown>
        {sports.map(sport => (
          <MenuItem key={sport}>{sport}</MenuItem>
        ))}
      </MenuDropdown>
    </Menu>
  )
}

```
- If we didn't compound using `children`, then we would have to define a state in `<Menu>` and pass it to `<MenuButton>` and `<MenuDropdown>`. 
-  This allows fine grain control 

The code you provided for `Menu`, `MenuButton`, `MenuDropdown`, and `MenuItem` is a classic illustration of the **Compound Components** pattern in React. This pattern is a powerful way to build flexible and reusable UI components that work together as a cohesive unit.

### 1. What are Compound Components?

Compound components are a set of related components that ==implicitly share state== and logic to achieve a common goal. Instead of passing all necessary props down to deeply nested children (which leads to prop drilling), the parent component (the "compound" component, e.g., `Menu`) provides a context or mechanism for its children to access shared state and functions.

They allow you to:

- **Decouple:** Separate the concerns of the overall component (e.g., `Menu`'s open/close state) from its individual parts (e.g., `MenuButton`'s click handling, `MenuItem`'s rendering).
    
- **Compose:** Use `props.children` to arrange the sub-components (`MenuButton`, `MenuDropdown`, `MenuItem`) in any order or combination that makes sense for your UI.
    
- **Simplify Usage:** The usage in JSX becomes highly declarative and intuitive, resembling native HTML elements (e.g., `<select><option></option></select>`).
    
### 2. Core Principles Demonstrated by  Example:

Let's look at how this example embodies these principles:
- **Composition via `props.children`:**
    - The `Menu` component renders `{children}`:[^eg]
        ```js
        // Menu.jsx
        return (
            <div className="menu">
                {children} {/* Renders MenuButton and MenuDropdown */}
            </div>
        )
        ```
        
    - The `MenuDropdown` (assuming it exists and also renders its children) renders `{children}`:
        ```js
        // MenuDropdown.jsx (conceptual)
        return (
            <div className="menu-dropdown">
                {children} {/* Renders MenuItem components */}
            </div>
        )
        ```
    - This allows you to define the structure of the menu directly in your `App` component's JSX, giving you full control over the order and content of the sub-components.
        
- **Implicit Relationship/Communication (The "Magic" of Compound Components):**
    
    - In the example, the `Menu` component has `open` state and a `toggle` function. For `MenuButton` to open/close the `MenuDropdown`, it needs access to this `open` state and `toggle` function.
        
    - **Crucially, you are NOT passing `open` and `toggle` as props directly to `MenuButton` or `MenuDropdown` in the `App` component.** This is where the "implicit" communication comes in. The sub-components know they are part of a `Menu` and can access its shared state.
        
- **Separation of Concerns:**
    - `Menu.jsx`: Manages the overall menu container and its open/closed state.
    - `MenuButton.jsx`: Responsible for the clickable element that controls the menu's visibility. It's a thin wrapper around a generic `Button` component, allowing for custom content.
    - `MenuItem.jsx`: Responsible for rendering an individual item within the dropdown.
    - This modularity makes each piece easier to reason about and test independently.
        
### 3. Benefits of this Approach:
- **Flexibility and Reusability:**
    - You can arrange `MenuButton` and `MenuDropdown` (and any other custom elements) in any order within `Menu`.
    - The sub-components themselves (`MenuButton`, `MenuItem`) are generic and can be reused in other contexts if needed.

- **Improved Readability and Developer Experience (DX):**
    - The JSX usage in `App.js` is highly semantic and readable, mimicking native HTML structures. It clearly describes the UI's intent.
    - Developers using your `Menu` component are guided by the structure, making it intuitive to use correctly.
        
- **Avoids Prop Drilling:**
    - This is a primary benefit. Instead of passing `open` and `toggle` down through `MenuButton` to `MenuDropdown` (if `MenuDropdown` were nested deeper), the Compound Component pattern allows sub-components to "reach up" and access the shared state directly.
        
- **Maintainability:**
    - Changes to the internal logic of `Menu` (e.g., how `open` state is managed) don't necessarily require changes to how `MenuButton` or `MenuItem` are defined, as long as the shared interface remains consistent.
        

### 4. How to Implement Implicit Communication (The "How-To"):

While the example _shows_ the structure, for `MenuButton` to actually _toggle_ the `MenuDropdown`'s visibility, the `Menu` component needs to share its `open` state and `toggle` function with its children. The two primary methods for this in Compound Components are:

#### a) React Context API (Most Common and Recommended)

This is the standard and most robust way to share state implicitly.

1. **Create a Context:**
    
    ```js
    // MenuContext.js
    import React, { createContext, useContext } from 'react';
    
    const MenuContext = createContext(null); // Default value can be anything
	
	// not neccessary, you can directly use useContext
    export function useMenuContext() {
      const context = useContext(MenuContext);
      if (!context) {
        throw new Error('useMenuContext must be used within a MenuProvider');
      }
      return context;
    }
    
    export default MenuContext;
    ```
    
2. **Provide the Context in the Parent Component (`Menu.jsx`):**
    
    ```js
    // Menu.jsx
    import React, { useState } from 'react';
    import MenuContext from './MenuContext'; // Import the context
    
    export default function Menu({ children }) {
      const [open, setOpen] = useState(false); // Initial state for open/close
    
      const toggle = () => {
        setOpen(prevOpen => !prevOpen);
      };
    
      const menuContextValue = {
        open,
        toggle,
        // Add any other shared state or functions here
      };
    
      return (
        <MenuContext.Provider value={menuContextValue}>
          <div className="menu">
            {children}
          </div>
        </MenuContext.Provider>
      );
    }
    ```
    
3. **Consume the Context in Child Components (`MenuButton.jsx`, `MenuDropdown.jsx`):**
    
    ```js
    // MenuButton.jsx
    import React from 'react';
    import { useMenuContext } from './MenuContext'; // Import the hook
    import Button from './Button'; // Assuming you have a generic Button component
    
    export default function MenuButton({ children, ...props }) {
      const { toggle } = useMenuContext(); // Access toggle from context
    
      return (
        <Button onClick={toggle} {...props}>
          {children}
        </Button>
      );
    }
    
    // MenuDropdown.jsx (conceptual)
    import React from 'react';
    import { useMenuContext } from './MenuContext';
    
    export default function MenuDropdown({ children }) {
      const { open } = useMenuContext(); // Access open state from context
    
      if (!open) return null; // Don't render if menu is closed
    
      return (
        <div className="menu-dropdown">
          {children}
        </div>
      );
    }
    ```
    

#### b) `React.cloneElement` (Less Common for State, More for Prop Injection)

This method involves iterating over `props.children` and cloning each child element, injecting additional props into them. It's less common for sharing dynamic state like `open/toggle` across multiple children, but useful if you just need to pass a specific prop or two down to _direct_ children.

```js
// Menu.jsx (using cloneElement - less ideal for this specific state sharing)
import React, { useState } from 'react';

export default function Menu({ children }) {
  const [open, setOpen] = useState(false);

  const toggle = () => {
    setOpen(prevOpen => !prevOpen);
  };

  return (
    <div className="menu">
      {React.Children.map(children, child => {
        // Only clone specific children that need the props
        if (child.type === MenuButton) {
          return React.cloneElement(child, { onClick: toggle });
        }
        if (child.type === MenuDropdown) {
          return React.cloneElement(child, { open });
        }
        return child; // Return other children as is
      })}
    </div>
  );
}
```

_Note: This approach can become cumbersome quickly if you have many types of children or complex state to share. Context is generally preferred for state management in compound components._

### 5. When to Use Compound Components:

- **Complex UI Widgets:** When building components like `Tabs`, `Accordion`, `Select`, `Modal`, `Tooltip`, `DatePicker`, where multiple sub-components need to coordinate their behavior and share state.
    
- **Improving API Readability:** When you want the usage of your component to be highly declarative and semantic in JSX.
    
- **Avoiding Prop Drilling:** When a parent component's state needs to be accessed by deeply nested children without explicitly passing props through every intermediate layer.
    
- **Encouraging Correct Usage:** By providing specific sub-components, you guide developers on how to construct the UI correctly.
    

### 6. When Not to Use Compound Components:

- **Simple Components:** For components that don't have complex internal state or multiple interacting parts, a simple component with props is sufficient. Over-engineering with compound components can add unnecessary complexity.
    
- ==**Global State:** For truly global application state (like user authentication or theme settings that affect almost every part of your app), a dedicated global state management solution (like Redux, Zustand, or even a single, higher-level Context) might be more appropriate. Compound components are best for localized, feature-specific state.==
    
By understanding and applying the Compound Components pattern, especially with the React Context API, you can build robust, flexible, and maintainable UI components that scale well in larger applications.



---
## References
[[React Context]]