
2025-06-25 18:45

Status:

Tags:

---
# Exporting and Importing components in React - Composability

## 🧱 What Is Composability?

> In React, **composability** means creating small, focused components and combining them together to form complex UIs.

To enable this, React uses **exporting and importing** of components between files.

---

## ✅ 1. **Exporting Components**

There are **two ways** to export components in React:

### a. **Default Export** (most common)

```jsx
// Header.js
function Header() {
  return <h1>Welcome</h1>;
}
export default Header;
```

### b. **Named Export**

```jsx
// Footer.js
export function Footer() {
  return <footer>© 2025</footer>;
}
```

You can also do:

```jsx
function Footer() {
  return <footer>© 2025</footer>;
}
export { Footer };
```

---

## ✅ 2. **Importing Components**

### a. **Importing Default Exports**

```jsx
import Header from './Header'; // no curly braces
```

You can rename default exports without `as`:

```jsx
import SomethingElse from './Header';
```
### b. **Importing Named Exports**

```jsx
import { Footer } from './Footer'; // uses curly braces
```

You can also **rename on import**:

```jsx
import { Footer as AppFooter } from './Footer';
```

---
## paths 
You can import any way with or without extension

```jsx
import { Footer as AppFooter } from './Footer';
import { Footer as AppFooter } from './Footer.js';
import { Footer as AppFooter } from './Footer.jsx';
```

All of them are valid. 

---
## 🧩 Example of Composability

Imagine this project structure:

```
src/
├── App.js
├── Header.js
├── Footer.js
└── Row.js
```

### ✅ Each component:

**Header.js**

```jsx
function Header() {
  return <h1>Netflix</h1>;
}
export default Header;
```

**Footer.js**

```jsx
export function Footer() {
  return <footer>© Netflix 2025</footer>;
}
```

**Row.js**

```jsx
export default function Row({ title }) {
  return <h2>{title}</h2>;
}
```

---

### ✅ App.js (Composing Components)

```jsx
import Header from './Header';
import { Footer } from './Footer';
import Row from './Row';

function App() {
  return (
    <div>
      <Header />
      <Row title="Trending Now" />
      <Footer />
    </div>
  );
}

export default App;
```

---

## 🧠 Why This Matters for Composability

|Feature|What It Enables|
|---|---|
|Exporting components|Let others reuse your logic/UI|
|Importing components|Build screens by composing smaller parts|
|Separate files/modules|Better organization & collaboration|

---

## ✅ Tip:

- Use **default export** when the file contains one primary component.
    
- Use **named exports** if you want to export multiple utilities or components from the same file.
    


---
## References