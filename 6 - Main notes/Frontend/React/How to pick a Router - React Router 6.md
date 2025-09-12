
2025-08-28 00:26

Status:

Tags:[React Router](3%20-%20Tags/React%20Router.md)

---
# How to pick a Router - React Router 6
https://reactrouter.com/6.30.1/routers/picking-a-router
In **React Router v6**, there are several types of routers, each designed for a specific rendering environment or use case. Let’s go through them:

---

## 🔄 1. **BrowserRouter**

> Uses the **HTML5 history API** for clean URLs (without hash `#`).

```jsx
import { BrowserRouter } from 'react-router-dom';

<BrowserRouter>
  <App />
</BrowserRouter>
```

 ✅ Use When:

- You are building a **regular web app** served from a single origin.
    
- You want **clean URLs** like `/about`, not `#/about`.

❌ Needs server configured to handle all routes (e.g., with `index.html` fallback)

> **Recommended** for apps hosted on Netlify, Vercel, or your own server.

---

## 🧭 2. **HashRouter**

> Uses the **URL hash (`#`)** to simulate routing.

```jsx
import { HashRouter } from 'react-router-dom';

<HashRouter>
  <App />
</HashRouter>
```

 ✅ Use When:

- You're deploying to **static file hosts** (like GitHub Pages).
    
- You don’t have server-side support for handling different routes.

🔗 URL looks like: `example.com/#/about`

> Use this when you **can’t configure the server** to handle routes.

---

## 🛠️ 3. **MemoryRouter** - Unit Testing or React Native

> Stores the navigation **in memory** (not reflected in the address bar).

```jsx
import { MemoryRouter } from 'react-router-dom';

<MemoryRouter initialEntries={['/login']} initialIndex={0}>
  <App />
</MemoryRouter>
```

### ✅ Use When:

- Writing **tests**.
    
- Building **non-browser environments** (e.g., React Native, Electron).
    

---

## 🧪 4. **StaticRouter**

> For **server-side rendering (SSR)** — navigation doesn't happen on the client.

```jsx
import { StaticRouter } from 'react-router-dom/server';

<StaticRouter location="/about">
  <App />
</StaticRouter>
```

### ✅ Use When:

- You're doing **server-side rendering** (e.g., using frameworks like Remix or custom SSR).
    

---

## 🧬 5. **createBrowserRouter / RouterProvider** (Data Router API)

> Introduced in **React Router v6.4+** — for route-based data loading.

```jsx
import { createBrowserRouter, RouterProvider } from 'react-router-dom';

const router = createBrowserRouter([...routes]);

<RouterProvider router={router} />
```

### ✅ Use When:

- You’re using **loaders, actions, deferred data, route error boundaries**, etc.
    
- Building more complex or full-stack-like apps.
    

---

## 📦 Summary Table
|Use Case|Router to Use|
|---|---|
|Standard React Web App|`BrowserRouter`|
|Static Hosting (e.g. GitHub)|`HashRouter`|
|Tests or Non-DOM Environments|`MemoryRouter`|
|Server-Side Rendering|`StaticRouter`|
|Loaders, Actions, Error Boundaries|`createBrowserRouter` + `RouterProvider`|

---

Let me know if you'd like a visual routing tree example or when to choose between traditional routers vs data routers.

---
## References