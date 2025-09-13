
2025-08-16 11:56

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

---
# Common Challenges in React apps and approaches
- [ ] Common challenges in React applications—**Routing**, **Data Fetching**, **Code Splitting**, **Performance Optimization**, and **Styling**—have various approaches depending on the scale, complexity, and tooling choices of the project

## 1. 🧭 **Routing**
Routing determines what content or pages to display when a user visits a particular URL. You need to set up a ==router to **map URLs to different parts of your app**.== You’ll also need to handle nested routes, route parameters, and query parameters. Routers can be configured within your code, or defined based on your component folder and file structures.

Routers are a core part of modern applications, and are usually integrated with data fetching (including prefetching data for a whole page for faster loading), code splitting (to minimize client bundle sizes), and page rendering approaches (to decide how each page gets generated).
### 🔸 Common Approaches

- **Manual Routing (Low-level)**: Using browser APIs like `window.location` and `history.pushState`.
- **Client-side Routing**: All routes handled on the client after the first page load.
- **Server-side Routing**: Server handles routes (common in traditional web apps or Next.js).
- **Data-aware routing** (loaders/actions coupled to routes)
- **Nested/layout routing** (route trees with shared layouts)
### ✅ Solutions in React Ecosystem

- **React Router**
    - Most widely used library.
    - Provides dynamic routing, nested routes, and lazy loading support.
        It enables:
		- **Client-side routing** (change views without full reload)
		- **Dynamic routes** (e.g., `/posts/:id`)
		- **Nested routes** (render child components within parent routes)
		- **Loader and actions** (in React Router v6.4+, for data fetching and mutations)
```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';

<BrowserRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
  </Routes>
</BrowserRouter>

```
- **Next.js Routing**
    - File-based routing.
    - Supports dynamic routes, API routes, middleware, and more.
        
- **Remix**
    - Focuses on nested routes + data loading per route.
    - Server-first routing model.
        
- **Reach Router** _(archived, now merged with React Router)_.

**When to pick**
- **Pure SPA** (no SSR needed): React Router or TanStack Router.
- **SEO/Perf/Edge rendering**: Next.js.
- **Form-heavy apps with web fundamentals**: Remix.
- **Type-safety fan**: TanStack Router or Next.js + TypeScript.

## 2. **Data Fetching**

- Fetching data from server. 
- Proper fetching means handling loading states, error states, and caching the fetched data, which can be complex.
Purpose-built data fetching libraries do the hard work of fetching and caching the data for you, letting you focus on what data your app needs and how to display it. These libraries are typically used directly in your components, but can also be integrated into routing loaders for faster pre-fetching and better performance, and in server rendering as well.

Note that ==fetching data directly in components can lead to slower loading times== due to network request waterfalls, so we recommend prefetching data in router loaders or on the server as much as possible! This allows a page’s data to be fetched all at once as the page is being displayed.
### ❓ The Problem:

How do you retrieve data from a server and manage loading/error states?
### 🔸 Common Approaches

- **Manual Fetching**
    - Using `fetch`, `axios`, or `XMLHttpRequest` in `useEffect`.
```jsx
useEffect(() => {
  fetch('/api/posts')
    .then(res => res.json())
    .then(setPosts)
    .catch(setError);
}, []);

```
- **Global State Fetching**
    - Fetching data in Redux or other state managers.
        
- **Server-side or Static Fetching**
    - Preloading data during build time or on the server (for SSR/SSG).

### ✅ Solutions in React Ecosystem

- **React Query / TanStack Query**
    - Declarative hooks for async state.
    - Handles caching, background sync, pagination, retries.
        
- **Redux Toolkit + RTK Query**
    - API slice to fetch and cache data via Redux.
        
- **SWR (by Vercel)** -  stale-while-revalidate , a HTTP cache invalidation
    - Lightweight and focused on revalidation + caching.
        
- **Next.js Data Fetching**
    - `getServerSideProps`, `getStaticProps`, and `getInitialProps`.
        
- **Remix Loaders**
    - Route-based data loaders using the loader API.
        
- **Apollo Client**
    - For GraphQL APIs with caching and normalization.

**When to pick**

- **SPA, varied endpoints**: TanStack Query.
- **Next.js (App Router)**: fetch in Server Components + Suspense; TanStack Query for client interactions.
- **Form posting + web fundamentals**: Remix loaders/actions.
- **GraphQL backend**: Apollo/urql/Relay (Relay for large, complex graphs

## 3. 📦 **Code Splitting**
- Loading smaller bundles of the app as per demand.

Code-splitting is the process of breaking your app into smaller bundles that can be loaded on demand. An app’s code size increases with every new feature and additional dependency. Apps can become slow to load because all of the code for the entire app needs to be sent before it can be used. ==Caching, reducing features/dependencies, and moving some code to run on the server can help mitigate slow loading but are incomplete solutions that can sacrifice functionality if overused.==

Similarly, if you rely on the apps using your framework to split the code, you might encounter situations where loading becomes slower than if no code splitting were happening at all. For example, [lazily loading](https://react.dev/reference/react/lazy) a chart delays sending the code needed to render the chart, splitting the chart code from the rest of the app. [](https://parceljs.org/recipes/react/#code-splitting). However, if the chart loads its data _after_ it has been initially rendered you are now waiting twice. This is a waterfall: rather than fetching the data for the chart and sending the code to render it simultaneously, you must wait for each step to complete one after the other.
### ❓ The Problem:
As apps grow, the JS bundle becomes large and slows down initial load.

### 🧠 Common Approaches:
- Manually using `import()` and Webpack's dynamic imports.
```jsx
import('./MyComponent').then((module) => {
  const MyComponent = module.default;
});
```
- **Manual Lazy Loading**
	- Splitting via `React.lazy` and `Suspense`.
- **Dynamic Imports**
	- Using dynamic `import()` to reduce initial bundle size.

### ✅ React Ecosystem Solution: **React.lazy + Suspense**
- **React.lazy + Suspense**
    - Native support for component-level lazy loading.
- **React Router Code Splitting**
    - Supports lazy loading route components.
- **Next.js Code Splitting**
    - Automatic per-page and dynamic import splitting.
- **Loadable Components**
    - More advanced code-splitting with SSR support.
- **Vite / Webpack**
    - Tree-shaking and chunk splitting at the bundler level.
- Lazily load components only when they’re needed.
    
```jsx
const LazyComponent = React.lazy(() => import('./LazyComponent'));

<Suspense fallback={<div>Loading...</div>}>
  <LazyComponent />
</Suspense>
```
- Tools like **Vite**, **Next.js**, or **Create React App** can also handle code splitting automatically via dynamic imports.
## 4. 🚀 **Performance Optimization**

### ❓ The Problem:
How do you keep your app fast and avoid unnecessary renders?

### 🧠 Common Approaches:
- Memoizing functions and values manually
- Debouncing expensive operations

### ✅ React Ecosystem Solutions:
- **React.memo**: Prevents re-renders of functional components if props haven't changed.
    
- **useMemo & useCallback**: Memoize values or functions.
    
- **React Profiler**: Analyze render performance.
    
- **useTransition**: Allows React to keep the app responsive during expensive updates.
    
- **useDeferredValue**: Helps with low-priority updates.

- **Next.js Image and Script Optimization**
    - Automatically optimize images and third-party scripts.
        
- **React Fast Refresh**
    - Enables better DX and speeds up hot-reloads during dev.
    
`const memoizedValue = useMemo(() => computeExpensiveValue(data), [data]);`

- Libraries like **Recoil**, **Zustand**, or **Redux Toolkit** help manage state with fewer re-renders when done properly.

## 5. 🎨 **Styling**

### ❓ The Problem:

How do you style components in a modular, reusable, and scalable way?

### 🧠 Common Approaches:

- **CSS / SCSS Files**
    - Traditional style sheets.
        
- **CSS Modules**
    - Locally scoped CSS with `module.css`.
        
- **CSS-in-JS**
    - Styling within components using JavaScript.

### ✅ React Ecosystem Solutions:

- **Styled-components / Emotion**
    - Popular CSS-in-JS libraries with theming, SSR, and dynamic styling.
        
- **Tailwind CSS**
    - Utility-first CSS framework.
    - Works well with React + frameworks like Next.js.
        
- **CSS Modules**
    - Built-in with Create React App and Next.js.
        
- **Vanilla Extract / Linaria**
    - Compile-time CSS-in-JS for better performance.
        
- **Stitches / Astroturf**
    - Modern alternatives for styling with zero-runtime overhead.
        
- **Material UI (MUI) / Chakra UI / Ant Design**
    - Component libraries with built-in styling solutions.

## Improving Application Performance [](https://react.dev/learn/build-a-react-app-from-scratch#improving-application-performance%20"Link%20for%20Improving%20Application%20Performance")
Since the build tool you select only support single page apps (SPAs) you’ll need to implement other [rendering patterns](https://www.patterns.dev/vanilla/rendering-patterns) like server-side rendering (SSR), static site generation (SSG), and/or React Server Components (RSC). Even if you don’t need these features at first, in the future there may be some routes that would benefit SSR, SSG or RSC.

- **Single-page apps (SPA)** load a single HTML page and dynamically updates the page as the user interacts with the app. SPAs are easier to get started with, but they can have slower initial load times. SPAs are the default architecture for most build tools.
    
- **Streaming Server-side rendering (SSR)** renders a page on the server and sends the fully rendered page to the client. SSR can improve performance, but it can be more complex to set up and maintain than a single-page app. With the addition of streaming, SSR can be very complex to set up and maintain. See [Vite’s SSR guide](https://vite.dev/guide/ssr).
    
- **Static site generation (SSG)** generates static HTML files for your app at build time. SSG can improve performance, but it can be more complex to set up and maintain than server-side rendering. See [](https://vite.dev/guide/ssr.html#pre-rendering-ssg).
    
- **React Server Components (RSC)** lets you mix build-time, server-only, and interactive components in a single React tree. RSC can improve performance, but it currently requires deep expertise to set up and maintain. See [Parcel’s RSC examples](https://github.com/parcel-bundler/rsc-examples).
Your rendering strategies need to integrate with your router so apps built with your framework can choose the rendering strategy on a per-route level. This will enable different rendering strategies without having to rewrite your whole app. For example, the landing page for your app might benefit from being statically generated (SSG), while a page with a content feed might perform best with server-side rendering.

- [ ]([Time%20to%20First%20Byte)), the first piece of content to render ([First Contentful Paint](https://web.dev/articles/fcp)), and the largest visible content of the app to render ([Largest Contentful Paint](https://web.dev/articles/lcp)).

## Summary Table

| Problem        | Common Approach               | React Ecosystem Solution                             |
| -------------- | ----------------------------- | ---------------------------------------------------- |
| Routing        | Hash/manual routing           | `react-router-dom`                                   |
| Data Fetching  | `fetch`, `axios`, `useEffect` | `React Query`, `SWR`, `Relay`, React Router loaders  |
| Code Splitting | `import()`                    | `React.lazy` + `Suspense`                            |
| Performance    | Manual memoization            | `React.memo`, `useMemo`, `Profiler`, `useTransition` |
| Styling        | Inline CSS / global CSS       | CSS Modules, Styled Components, Tailwind             |


---
## References
https://react.dev/learn/build-a-react-app-from-scratch
