
2025-06-27 18:18

Status:

Tags: [React](../../../3%20-%20Tags/React.md) 

---
# Handling Static assets(like Images) in React

## 📁 Where to Put Static Assets in React?

There are **two main places** you can store static assets in a React app:

---

### ✅ 1. `public/` folder

- Files in `public/` are served **as-is**.
    
- Use when you need a file to be available at a **specific path**.
    

📂 Example:

```
public/
├── logo.png
├── resume.pdf
└── index.html
```

### 🔹 Usage in code:

```jsx
<img src="/logo.png" alt="Logo" />
<a href="/resume.pdf" download>Download Resume</a>
```

> ✅ React doesn't process files in `public/`, so they must be referenced by absolute path (`/filename.ext`).

---

### ✅ 2. `src/` folder

- Use for assets that are **imported or processed by Webpack/Vite**.
    
- Recommended for images used **inside components**.
    

📂 Example:

```
src/
├── assets/
│   └── banner.jpg
├── components/
│   └── Hero.jsx
```

### 🔹 Usage in code:

```jsx
import banner from '../assets/banner.jpg';

function Hero() {
  return <img src={banner} alt="Banner" />;
}
```

> ✅ Works well with Vite/Webpack – asset is optimized & cache-busted.

---

## 🧠 When to Use Which?

|Folder|Use Case|Example|
|---|---|---|
|`public/`|Static files with direct access or links|`<img src="/logo.png" />`|
|`src/`|Component-related assets|`import img from './img.png'`|

---

## 🎯 Special Notes

### ✅ Fonts:

- Place in `public/fonts` or `src/assets/fonts`
    
- Reference via CSS:
    

```css
@font-face {
  font-family: 'MyFont';
  src: url('/fonts/MyFont.woff2') format('woff2');
}
```

### ✅ Favicon:

Place it in `public/` and reference it in `public/index.html`.

---

## 🧠 TL;DR

|Asset Type|Folder|Reference Example|
|---|---|---|
|Image|`public/`|`<img src="/logo.png" />`|
|Image|`src/`|`import logo from './logo.png'`|
|PDF|`public/`|`<a href="/resume.pdf">Download</a>`|
|Font|`public/` or `src/`|`@font-face` in CSS|

---
## References
[Why should we import Assets instead of using its path - React](Why%20should%20we%20import%20Assets%20instead%20of%20using%20its%20path%20-%20React.md)