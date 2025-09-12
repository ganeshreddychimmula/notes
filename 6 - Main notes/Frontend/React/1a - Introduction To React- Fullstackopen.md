
2025-07-14 18:02

Status:

Tags: [React](3%20-%20Tags/React.md)

---
# 1a - Introduction To React- Fullstackopen

### Create a React project using Vite
[^1]
```bash
# npm 6.x (outdated, but still used by some):
npm create vite@latest introdemo --template react

# npm 7+, extra double-dash is needed:
npm create vite@latest introdemo -- --template react
```

```bash
cd introdemo
npm install
```

```bash
npm run dev
```

### Component
[Creating a React Component](6%20-%20Main%20notes/Frontend/React/Creating%20a%20React%20Component.md)
```js
ReactDOM.createRoot(document.getElementById('root')).render(<App />)
```
renders its contents into the _div_-element, defined in the file _index.html_, having the _id_ value 'root'.

The first rule of frontend web development:

> _keep the console open all the time_> 

### JSX
[(2) JSX React](6%20-%20Main%20notes/Frontend/React/(2)%20JSX%20React.md) 
It seems like React components are returning HTML markup. However, this is not the case. The layout of React components is mostly written using [JSX](https://react.dev/learn/writing-markup-with-jsx). Although JSX looks like HTML, we are dealing with a way to write JavaScript. Under the hood, JSX returned by React components is compiled into JavaScript.
- It is also possible to write React as "pure JavaScript"(using createReact) without using JSX. Although, nobody with a sound mind would do so.
- In practice, JSX is much like HTML with the distinction that with JSX you can easily embed dynamic content by writing appropriate JavaScript within curly braces. The idea of JSX is quite similar to many templating languages, such as Thymeleaf used along with Java Spring, which are used on servers.
- JSX is "[XML](https://developer.mozilla.org/en-US/docs/Web/XML/XML_introduction)-like", which means that every tag needs to be closed.
- Indeed, a core philosophy of React is composing applications from many specialized reusable components.[^2]
### props: passing data to components
[Props - React](6%20-%20Main%20notes/Frontend/React/Props%20-%20React.md)

### Possible error message

Depending on the editor you are using, you may receive the following error message at this point:

![screenshot of vs code showing eslint error: "name is missing in props validation"](https://fullstackopen.com/static/d0f3c768a0844c92d98335a23ab9d748/5a190/1-vite5.png)

It's not an actual error, but a warning caused by the [ESLint](https://eslint.org/) tool. You can silence the warning [react/prop-types](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/prop-types.md) by adding to the file _eslint.config.js_ the next line

```js
export default [
  { ignores: ['dist'] },
  {
    files: ['**/*.{js,jsx}'],
    languageOptions: {
      ecmaVersion: 2020,
      globals: globals.browser,
      parserOptions: {
        ecmaVersion: 'latest',
        ecmaFeatures: { jsx: true },
        sourceType: 'module',
      },
    },
    settings: { react: { version: '18.3' } },
    plugins: {
      react,
      'react-hooks': reactHooks,
      'react-refresh': reactRefresh,
    },
    rules: {
      ...js.configs.recommended.rules,
      ...react.configs.recommended.rules,
      ...react.configs['jsx-runtime'].rules,
      ...reactHooks.configs.recommended.rules,
      'react/jsx-no-target-blank': 'off',
      'react-refresh/only-export-components': [
        'warn',
        { allowConstantExport: true },
      ],
      'react/prop-types': 0,    },
  },
]
```

> **First letter of React component names must be capitalized**.

```js
const App = () => {
  return (
    <div>
      <h1>Greetings</h1>
      <Hello name='Maya' age={26 + 10} />
      <footer /> // react component 
	</div>
  )
}
```

the page is not going to display the content defined within the footer component, and instead React only creates an empty [footer](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer) element, i.e. the built-in HTML element instead of the custom React element of the same name.

### Do not render objects
Consider an application that prints the names and ages of our friends on the screen:

```js
const App = () => {
  const friends = [
    { name: 'Peter', age: 4 },
    { name: 'Maya', age: 10 },
  ]

  return (
    <div>
      <p>{friends[0]}</p>
      <p>{friends[1]}</p>
    </div>
  )
}

export default App
```

However, nothing appears on
![devtools showing error with highlight around "Objects are not valid as a React child"](https://fullstackopen.com/static/fdcc65efff174e0c0ce15bf636c4cd1c/5a190/34new.png)

The core of the problem is _==Objects are not valid as a React child_==, i.e. the application tries to render _objects_ and it fails again.

In React, the individual things rendered in braces must be **primitive values**, such as numbers or strings.

A small additional note to the previous one. ==React also allows arrays to be rendered==_ if_ the array contains values ​​that are eligible for rendering (such as numbers or strings). So the following program would work, although the result might not be what we want:
```js
const App = () => {
  const friends = [ 'Peter', 'Maya']

  return (
    <div>
      <p>{friends}</p>
    </div>
  )
}
```


---
## References
[^1]: [Setting Up React Locally with Vite](2%20-%20Source%20Material/FrontEnd%20Material/React/Setting%20Up%20React%20Locally%20with%20Vite.md)
[^2]: [Composability in React and why its important](6%20-%20Main%20notes/Frontend/React/Composability%20in%20React%20and%20why%20its%20important.md)
