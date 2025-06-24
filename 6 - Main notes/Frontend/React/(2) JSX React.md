
2025-06-24 18:00

Status:

Tags: [[React]]

---
# JSX React
It seems like React components are returning HTML markup. However, this is not the case. The layout of React components is mostly written using [JSX](https://react.dev/learn/writing-markup-with-jsx). Although JSX looks like HTML, we are dealing with a way to write JavaScript. **Under the hood, JSX returned by React components is compiled into JavaScript.**
- JSX is "[XML](https://developer.mozilla.org/en-US/docs/Web/XML/XML_introduction)-like", which means that every tag needs to be closed. 
```html
<br>
```

but when writing JSX, the tag needs to be closed:

```html
<br />
```
- JSX is Syntactic sugar on CreateElement call.
- Under the hood React still takes JSX and makes a createElement call.
- It is not strict to use .jsx instead of .js but vite suggests due to its issues.
- Here are the benefits of JSX over `React.createElement` in brief:
 with `CreateElement`
```js
import React from 'react';
import ReactDOM from 'react-dom/client';

function AppWithCreateElement() {
  // Creating a paragraph element with text content
  return React.createElement(
   'p',// Type of element (paragraph)
   { className: 'my-text' }, // Props object (here, a CSS class)
   'Hello, World!' // Child content (plain text)
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(React.createElement(AppWithCreateElement, null)); // Render the component
```

 with `JSX`
```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';

function AppWithJSX() {
  // Creating a paragraph element with text content using JSX
  return (
    <p className="my-text">
      Hello, World!
    </p>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<AppWithJSX />); // Render the component
```


- **Readability & Maintainability:** JSX resembles HTML, making UI structures much easier to read, write, and understand compared to nested `React.createElement` calls. This significantly improves code clarity and maintainability.
- **Developer Experience (DX):** It's more intuitive and less verbose. Developers can write components more quickly and with fewer errors due to its familiar syntax.
- **Static Analysis & Tooling:** Because JSX is syntactically closer to JavaScript and can be statically analyzed, tools like linters and type checkers (e.g., ESLint, TypeScript) can provide better error checking, autocompletion, and warnings, leading to fewer bugs.
- **Performance (Compile-time Optimization):** While ultimately both compile down to `React.createElement` calls, the compilation step allows for potential optimizations that might be harder to achieve when manually writing `createElement`.
- **Visual Representation:** It provides a clearer visual representation of the UI hierarchy, making it easier to conceptualize the component tree.
JSX
```jsx
const App = () => {
  const now = new Date()
  const a = 10
  const b = 20
  console.log(now, a+b)

  return (
    <div>
      <p>Hello world, it is {now.toString()}</p>
      <p>
        {a} plus {b} is {a + b}
      </p>
    </div>
  )
}
```
CreateReact
```js
const App = () => {
  const now = new Date()
  const a = 10
  const b = 20
  console.log(now, a+b)

  return (
    <div>
      <p>Hello world, it is {now.toString()}</p>
      <p>
        {a} plus {b} is {a + b}
      </p>
    </div>
  )
}
```



  
---
## References
[[JSX elements must have a single common parent]]