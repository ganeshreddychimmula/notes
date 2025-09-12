
2025-06-24 17:55

Status:

Tags: [React](3%20-%20Tags/React.md) 

---
# CreateElement React

> Old Way
`React.createElement()` is a fundamental method in React used to create React elements. ==It is the underlying function that JSX,  While developers typically use JSX for writing React components==, `React.createElement()` offers an alternative for creating elements directly with JavaScript.

Syntax:

JavaScript

```jsx
React.createElement(type, [props], [...children])
```

Parameters:

- `type`:
    
    This specifies the type of element to be created. It can be:
    
    - A string representing an HTML tag name (e.g., `'div'`, `'span'`, `'h1'`).
    - A React component (either a class component or a functional component).
    - A special React component like `React.Fragment`.
    
- `props` (optional):
    
    An object containing properties (attributes) to assign to the element or component. These can include:
    
    - Standard HTML attributes (e.g., `className`, `style`, `id`).
    - Event handlers (e.g., `onClick`, `onChange`).
    - Custom data props.
    - If no props are needed, `null` or an empty object `{}` can be passed.
    
- `...children` (optional):
    
    Zero or more arguments representing the children of the element. These can be:
    
    - Other React elements created with `React.createElement()`.
    - Strings or numbers (for text content).
    - Arrays of React nodes.
    - `null`, `undefined`, `true`, or `false` (which are treated as empty nodes). 
    

Example:

To create a simple `div` element with a `className` and some text content using `React.createElement()`:

JavaScript

```jsx
import React from 'react';
const myDiv = React.createElement(  'div',  { className: 'my-class' },  'Hello, React!');
```

This `React.createElement()` call is equivalent to the following JSX:

Code

```jsx
<div className="my-class">Hello, React!</div>
```

Key Points:

- `React.createElement()` is the foundation upon which JSX builds.
- While JSX is generally preferred for its readability and conciseness, `React.createElement()` can be used directly for programmatic element creation or when JSX is not desired.
- It creates lightweight React elements, which are then used by React DOM (or other renderers) to build and manage the actual DOM.

---
## References

