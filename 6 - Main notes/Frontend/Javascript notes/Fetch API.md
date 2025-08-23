
2025-08-23 10:05

Status:

Tags: [[JavaScript]]

---
# Fetch API

## 1) What `fetch()` returns and why it’s “two‑stage”

- The simplest Fetch: involves making a GET request to retrieve data from a specified URL.
    - ↪️ A basic syntax `fetch(url)` initiates a GET request to the given `url`.
    - ↪️ This function call immediately starts network request and returns a promise.
        
- Fetch is fundamentally a 2-stage process for handling response.
    1. Promise returned by `fetch()` resolves not with final data, but with a `Response` object as soon as the server sends back the HTTP headers.
    2. Accessing the actual content requires another `async` operation.
        - ↪️ This design allows to inspect response metadata (like status, headers) before deciding how to proceed.
            

- `fetch(url[, options])` **starts** the network request immediately and returns a **Promise**.
    
- The promise **resolves** when the response headers arrive (not the full body). You then read the body via an **asynchronous** method: `.json()`, `.text()`, `.blob()`, `.arrayBuffer()`, `.formData()`, or by streaming from `response.body`.
    
- **Important**: `response.ok` is `true` only for HTTP **200–299**. Anything else (including 304) makes `ok === false`.
    
- **Body can be read once**. To read it twice (e.g., log & parse), use `response.clone()`.

- 
```js
const res = await fetch('/api/user');
if (!res.ok) throw new Error(`HTTP ${res.status}`);
const data = await res.json();
```

> Heads‑up: `response.json()` can itself **throw** if the body isn’t valid JSON.

---

## 2) Configuring requests (methods, headers, body, and more)

```js
await fetch(url, {
  method: 'POST',              // GET | POST | PUT | PATCH | DELETE | ...
  headers: {                   // or new Headers()
    'Content-Type': 'application/json',
    Accept: 'application/json'
  },
  body: JSON.stringify(payload),
  // other options below
});
```

### Common options you’ll actually use

- **`headers`**: keys are case‑insensitive. Some headers are **forbidden** to set (e.g., `Host`, `Content-Length`, `Connection`, `Cookie`); the browser manages those.
    
- **`body`** types: `string`, `Blob`, `FormData`, `URLSearchParams`, `ArrayBuffer`/`TypedArray`, `ReadableStream` (streaming upload; requires `{duplex: 'half'}` in supporting browsers).
    
- **`method`**: use `PATCH` for partial updates; `PUT` for full replacement.
    
- **`credentials`** (browser default is **`'same-origin'`**):
    
    - `'omit'` – never send cookies/HTTP auth.
        
    - `'same-origin'` – send for same origin only (default).
        
    - `'include'` – send for cross‑site too (CORS must allow credentials).
        
- **`mode`**: `'cors'` (default for cross‑origin), `'same-origin'`, `'no-cors'` (opaque responses; very limited).
    
- **`cache`**: `'default' | 'no-store' | 'reload' | 'no-cache' | 'force-cache' | 'only-if-cached'` (advisory hints—server `Cache-Control` still matters).
    
- **`redirect`**: `'follow'` (default), `'error'`, `'manual'` (results in an **opaqueredirect** response; limited access in browsers).
    
- **`referrer` / `referrerPolicy`**: control what Referer is sent.
    
- **`integrity`**: Subresource Integrity hash for tamper detection.
    
- **`keepalive`**: allow requests during page unload (best effort, small payloads).
    
- **`signal`**: for cancellation via `AbortController`.
    

### Sending JSON

```js
await fetch('/api/todos', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ title: 'Buy milk' })
});
```

### Sending forms & files

```js
const fd = new FormData(formEl); // or fd.append('file', fileObj)
await fetch('/upload', { method: 'POST', body: fd });
// Don’t set Content-Type manually; browser sets proper multipart boundary.
```

### Sending URL‑encoded data

```js
const params = new URLSearchParams({ q: 'cats', page: 1 });
await fetch('/search', {
  method: 'POST',
  headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
  body: params
});
```

---

## 3) Reading responses (and streaming)

- **Headers**: `response.headers.get('content-type')` (note: header names are case‑insensitive).
    
- **Body once** rule: use `.clone()` if you must read twice.
    
- **Stream large downloads** with the Web Streams API:
```js
const res = await fetch('/big-file');
const reader = res.body.getReader();
let received = 0;
while (true) {
  const { done, value } = await reader.read();
  if (done) break;
  received += value.byteLength;
  // process chunk "value" (Uint8Array)
}
```

### Download as Blob (then save)

```js
const res = await fetch('/report.pdf');
const blob = await res.blob();
const url = URL.createObjectURL(blob);
const a = Object.assign(document.createElement('a'), { href: url, download: 'report.pdf' });
a.click();
URL.revokeObjectURL(url);
```

---

## 4) Errors and retries (network vs HTTP)

- **`fetch()` rejects** the promise on **network failures** (DNS issues, offline, CORS preflight failure, TLS errors). It **does not** reject for HTTP errors (e.g., 404, 500) — check `res.ok`.
    
- Always handle **both**:
```js
async function safeJson(url, options) {
  const res = await fetch(url, options).catch(err => {
    // Network error (TypeError in browsers)
    throw new Error('Network failure: ' + err.message);
  });

  const type = res.headers.get('content-type') || '';
  const body = type.includes('application/json') ? await res.json().catch(() => ({})) : await res.text();

  if (!res.ok) {
    const detail = typeof body === 'string' ? body : JSON.stringify(body);
    const e = new Error(`HTTP ${res.status}: ${detail}`);
    e.response = res; e.body = body; throw e;
  }
  return body;
}
```

### Timeouts & cancellation

- Fetch has **no built‑in timeout**, but you can cancel:

```js
const c = new AbortController();
const t = setTimeout(() => c.abort(), 8000);
try {
  const res = await fetch('/slow', { signal: c.signal });
  // ...
} finally { clearTimeout(t); }
```

- Newer runtimes support **`AbortSignal.timeout(ms)`**: `{ signal: AbortSignal.timeout(8000) }`.
    

### Simple retry with backoff (respecting `Retry-After`)

```js
async function retryingFetch(url, options = {}, tries = 3) {
  let last;
  for (let i = 0; i < tries; i++) {
    try { return await fetch(url, options); }
    catch (e) { last = e; await new Promise(r => setTimeout(r, 2 ** i * 300)); }
  }
  throw last;
}
```

---

## 5) CORS in practice (quick mental model)

- **Same‑Origin Policy** blocks reading cross‑origin responses unless the server opts in via **CORS**.
    
- A request is **simple** (no preflight) if it uses `GET/HEAD/POST`, only simple headers, and simple content types. Otherwise the browser sends a **preflight** `OPTIONS` request.
    
- For credentialed cross‑site requests, you must set `credentials: 'include'` **and** the server must send `Access-Control-Allow-Credentials: true` (and not use `*` for `Allow-Origin`).
    
- If CORS fails, browsers typically surface a **`TypeError`** and hide details for security.
    

---

## 6) Auth, cookies, and CSRF hints

- With cookies (session auth), use:
    - same‑site: default `credentials: 'same-origin'` is fine for first‑party apps;
    - cross‑site: `credentials: 'include'` and server CORS must allow credentials.
        
- With bearer tokens (JWT/OAuth): put in **`Authorization: Bearer <token>`** header; don’t mix with `credentials: 'include'` unless you intend to send cookies as well.
    
- For CSRF‑protected forms, servers often require a custom header (e.g., `X-CSRF-Token`).
    

---

## 7) Redirects

- Default is **`redirect: 'follow'`** (up to ~20 hops). Some status codes (e.g., 301/302/303) may change the method to `GET` unless you set server/client otherwise.
    
- `redirect: 'manual'` returns an **opaqueredirect** in browsers — you can’t read headers like `Location` due to security; it’s mainly useful in service workers.
    

---

## 8) Performance & caching

- Respect HTTP caching headers (`Cache-Control`, `ETag`/`If-None-Match`, `Last-Modified`/`If-Modified-Since`).
    
- Use `cache: 'no-store'` for truly uncached requests (diagnostics, auth endpoints), otherwise prefer validator‑based caching.
    
- Combine with **Service Workers** & the **Cache Storage API** for offline/instant loads.
    

---

## 9) Upload progress (myth‑busting)

- Classic browser `fetch()` doesn’t expose **upload progress** events. Use **XHR** or stream the request body and implement server‑side progress endpoints. (Download progress is possible via streams.)
    

---

## 10) Content negotiation & detection

- Send `Accept` (e.g., `application/json`).
    
- Detect response type by inspecting `Content-Type`. Be robust to missing or incorrect types.
    

```js
const type = res.headers.get('content-type') || '';
if (type.includes('application/json')) {
  const data = await res.json();
} else if (type.startsWith('text/')) {
  const text = await res.text();
}
```

---

## 11) Practical cookbook

### A. GET with JSON + timeout + retries

```js
async function getJSON(url) {
  const res = await retryingFetch(url, { signal: AbortSignal.timeout(8000) });
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return res.json();
}
```

### B. POST JSON with robust error parsing

```js
async function postJSON(url, payload) {
  const res = await fetch(url, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json', Accept: 'application/json' },
    body: JSON.stringify(payload),
  });
  const ct = res.headers.get('content-type') || '';
  const body = ct.includes('json') ? await res.json().catch(() => ({})) : await res.text();
  if (!res.ok) throw new Error(`HTTP ${res.status}: ${typeof body === 'string' ? body : JSON.stringify(body)}`);
  return body;
}
```

### C. Abort on route change / component unmount (React)

```js
useEffect(() => {
  const c = new AbortController();
  fetch('/api/data', { signal: c.signal }).then(...).catch((e) => {
    if (e.name !== 'AbortError') console.error(e);
  });
  return () => c.abort();
}, []);
```

### D. File upload with extra fields

```js
const fd = new FormData();
fd.append('avatar', fileInput.files[0]);
fd.append('displayName', 'Ganesh');
await fetch('/profile', { method: 'POST', body: fd });
```

### E. Stream a large download to text incrementally

```js
const res = await fetch('/logs');
const reader = res.body.getReader();
const decoder = new TextDecoder();
let buf = '';
for (let chunk = await reader.read(); !chunk.done; chunk = await reader.read()) {
  buf += decoder.decode(chunk.value, { stream: true });
  // process lines in buf ...
}
buf += decoder.decode();
```

---

## 12) Node.js differences

- Node **v18+** includes `fetch`, `Headers`, `Request`, `Response` built‑in (via **undici**). No browser security model (no CORS); cookies aren’t sent automatically.
    
- File & `FormData` handling differs slightly (use `fs.readFile`, `Blob`, or `FormData` from `undici`/`formdata-node`).
    
- In CommonJS on older Node, you’d use `node-fetch`.
    

```js
// Node 18+
const res = await fetch('https://api.example.com/data');
```

---

## 13) Subtle correctness & clarifications

- **Forbidden headers** (browser‑set): e.g., `Accept-Charset`, `Accept-Encoding`, `Connection`, `Content-Length`, `Cookie`, `Host`, `Origin`, `Referer`, `Sec-*` headers.
    
- **204/205 No Content**: don’t call `.json()` unless you know the server still returns a body.
    
- **HEAD** returns headers only; body methods will resolve to empty.
    
- **`response.type`** can be `'basic' | 'cors' | 'opaque' | 'opaqueredirect'` and affects what you can read.
    
- **Redirect method normalization**: 301/302/303 may switch to `GET`; 307/308 preserve method & body.
    

---

## 14) Testing & tooling tips

- Use **MSW (Mock Service Worker)** to mock network in tests.
    
- In browsers, try requests in DevTools **Network** tab; watch CORS, cache, cookies, and timing.
    
- Lint for `no-unsafe-finally`/unhandled promises; log only sanitized error data (avoid leaking tokens).
    

---

## 15) Quick reference tables

### HTTP methods

|Method|Description|Safe|Idempotent|Cacheable|
|---|---|--:|--:|--:|
|GET|Retrieve resource representation|Yes|Yes|Yes|
|POST|Create/trigger action|No|No|Conditionally|
|PUT|Replace at URI|No|Yes|No|
|PATCH|Partial update|No|No|No|
|DELETE|Remove resource|No|Yes|No|
|HEAD|Headers only|Yes|Yes|Yes|
|OPTIONS|Capabilities / CORS preflight|Yes|Yes|No|

### Status codes (high level)

- **1xx** Informational
    
- **2xx** Success
    
- **3xx** Redirection (note: 304 is not “ok”)
    
- **4xx** Client error
    
- **5xx** Server error
    

### Common headers

- **Request**: `Authorization`, `Accept`, `Content-Type`, `If-None-Match`, `If-Modified-Since`, custom `X-*`/`Sec-*` (many `Sec-*` are browser-managed).
    
- **Response**: `Content-Type`, `Cache-Control`, `ETag`, `Last-Modified`, `Set-Cookie`, `Location`, `Retry-After`.
    

---

## 16) Mini‑exercises to cement understanding

1. **Write** a function that GETs JSON with a 5s timeout and retries twice.
    
2. **POST** a `FormData` upload and parse a JSON error when status is 400.
    
3. **Stream** a newline‑delimited JSON (NDJSON) endpoint and process objects as they arrive.
    
4. **Implement** a React effect that aborts in‑flight fetches on unmount.

---

## 17) Example
```js
async function robustFetch(url, options) {  
    let response;  
    try {  
        // Attempt the network request  
        response = await fetch(url, options);  
        if (!response.ok) { // Check for HTTP error  
            let errorMsg = `HTTP error! status: ${response.status}`;  
            let errorDetails = null;  
            try {  
                // Attempt to parse error details from the response body  
                // Check Content-type header if necessary to decide between json() or text()  
                if (response.headers.get('Content-type') && response.headers.get('Content-type').includes('application/json')) {  
                    errorDetails = await response.json();  
                    errorMsg += `, details: ${JSON.stringify(errorDetails)}`;  
                } else {  
                    errorDetails = await response.text();  
                    errorMsg += `, details: ${errorDetails}`;  
                }  
            } catch (error) {  
                // Ignore if parsing the error body fails.  
                console.warn("Could not parse the response body:", error);  
            }  
            // Create an error object that includes status & potentially parsed details.  
            const error = new Error(errorMsg);  
            error.response = response;  
            error.details = errorDetails;  
            throw error;  
        }  
        return await response.json(); // If response is ok, proceed to parse  
    } catch (error) {  
        // Re-throw errors (Fetch promise rejects)  
        console.error('Fetch operation failed:', error);  
        throw error;  
    }  
}  


robustFetch(url, {})  
    .then(data => console.log("User data:", data))  
    .catch(err => console.error("Houston, we have a problem:", err));**
```

---

### TL;DR

- Inspect `res.ok`/`res.status`; network failures vs HTTP errors are different.
    
- Use `AbortController` (or `AbortSignal.timeout`) for timeouts/cancellation.
    
- Don’t set `Content-Type` when sending `FormData`.
    
- For cross‑site cookies, set `credentials: 'include'` and configure CORS properly.
    
- Body is single‑use; clone if needed; stream when large.
---
## References
[[CORS (Cross-Origin Resource Sharing)]]