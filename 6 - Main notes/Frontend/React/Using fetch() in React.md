
2025-08-22 22:31

Status:

Tags: [[React]]

---
# Using `fetch()` in React — Notes & Best Practices

This guide explains how to use the Fetch API effectively in React, including lifecycle-aware data fetching, error handling, cleanup, and integration with modern hooks.

---

## 1) Basics of `fetch()` in React

- `fetch(url)` returns a promise that resolves to a `Response` object.
    
- Must be called **inside a side effect**, not directly in the component body.
    

---

## 2) Fetching data with `useEffect`

```jsx
import { useEffect, useState } from 'react';

function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch('https://api.example.com/users')
      .then(res => {
        if (!res.ok) throw new Error(`HTTP ${res.status}`);
        return resjs.on();
      })
      .then(data => setUsers(data))
      .catch(err => setError(err.message))
      .finally(() => setLoading(false));
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  return <ul>{users.map(u => <li key={u.id}>{u.name}</li>)}</ul>;
}
```

---

## 3) Using `async/await` in `useEffect`

- React doesn’t allow the `useEffect` callback itself to be async.
    
- Use an **inner async function**:
    

```jsx
useEffect(() => {
  const fetchData = async () => {
    try {
      const res = await fetch('https://api.example.com/users');
      if (!res.ok) throw new Error(`HTTP ${res.status}`);
      const data = await res.json();
      setUsers(data);
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  };
  fetchData();
}, []);
```

---

## 4) Abort fetch on unmount

- Prevent setting state after unmount to avoid memory leaks.
    
- Use `AbortController`:

```jsx
useEffect(() => {
  const controller = new AbortController();

  const fetchData = async () => {
    try {
      const res = await fetch('https://api.example.com/users', { signal: controller.signal });
      const data = await res.json();
      setUsers(data);
    } catch (err) {
      if (err.name !== 'AbortError') setError(err.message);
    } finally {
      setLoading(false);
    }
  };

  fetchData();
  return () => controller.abort();
}, []);
```

---

## 5) Refetching on dependency change

```jsx
useEffect(() => {
  const controller = new AbortController();
  const fetchData = async () => {
    setLoading(true);
    try {
      const res = await fetch(`https://api.example.com/items?page=${page}`, { signal: controller.signal });
      const data = await res.json();
      setItems(data);
    } catch (err) {
      if (err.name !== 'AbortError') setError(err.message);
    } finally {
      setLoading(false);
    }
  };

  fetchData();
  return () => controller.abort();
}, [page]);
```

---

## 6) When to extract to a custom hook

Create a reusable hook when:

- The same fetch logic is needed in multiple places
    
- You want separation of concerns
    

### Example: `useFetch`

```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const controller = new AbortController();
    const fetchData = async () => {
      try {
        const res = await fetch(url, { signal: controller.signal });
        if (!res.ok) throw new Error(`HTTP ${res.status}`);
        const json = await res.json();
        setData(json);
      } catch (err) {
        if (err.name !== 'AbortError') setError(err.message);
      } finally {
        setLoading(false);
      }
    };
    fetchData();
    return () => controller.abort();
  }, [url]);

  return { data, loading, error };
}
```

---

## 7) Error boundaries and fallback UI

- Consider combining `useFetch` with React Error Boundaries.
    
- Use fallback UIs for better user experience.
    

---

## 8) Alternative tools (when fetch isn't enough)

- **Axios**: Better error handling, request cancellation, interceptors.
    
- **SWR / React Query / TanStack Query**: Advanced caching, retries, polling, pagination, deduplication.
    

---

## 9) Quick tips

- Always check `res.ok`
    
- Never use async directly in `useEffect` callback
    
- Abort requests to avoid setting state after unmount
    
- Avoid race conditions by syncing state with latest request
    
- For complex apps, use libraries like React Query
    

---

## TL;DR

- Use `useEffect` for fetch
    
- Handle loading + error states
    
- Cancel requests with `AbortController`
    
- Extract logic to custom hook if reused
    
- Prefer `SWR` or `React Query` in real-world apps

---
## References
[[Fetch API]]