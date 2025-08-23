
2025-08-23 11:12

Status:

Tags: [[JavaScript]]

---
# CORS (Cross-Origin Resource Sharing) 


## 1) Why CORS exists

- **Default security rule (Same-Origin Policy / SOP):** A web page can’t freely read responses from another origin (different scheme, host, or port).
    
- This prevents malicious sites from stealing sensitive data by embedding requests to other sites.
    
- Problem: Modern apps often need to call APIs hosted on a different domain (e.g., frontend on `www.app.com` calling backend at `api.app.com`).
    
- **Solution:** CORS is a **standard mechanism** (endorsed by W3C) that lets servers explicitly say which origins are allowed to access their resources.
    
**Why CORS is needed?**

- While security provided by SOP (Same-Origin Policy) is invaluable, its default behavior of blocking cross-origin read poses a significant challenge for modern web applications.
    
- ↪️ We sometimes really need these interactions.
    
- Example:
    
    - A Single Page Application hosted on `www.my-app.com` needs to Fetch user data or perform actions via an API located at `api.my-app.com`.
        
    - The strict SOP would prevent the application from functionality correctly by blocking these necessary cross-origin requests

**CORS Definition**:

- Cross-Origin Resource Sharing (CORS) is the standard, W3C-endorsed mechanism designed to address this need.
    
- ↪️ It provides a controlled way for servers to relax the Same-Origin Policy for specific resources.
    
- ↪️ CORS operates through a system of HTTP headers exchanged between the browser & the server.
    
- ↪️ By using these headers, a server can explicitly inform the browser which origins, other than its own, are permitted to load resources from it.

---

## 2) How CORS works (mental model)

- Browser enforces SOP. When JS on page makes a cross-origin request:
    
    - Browser attaches an **`Origin` request header**.
        
    - Server decides if it’s allowed, and responds with CORS headers (e.g., `Access-Control-Allow-Origin`).
        
    - If allowed, browser passes the response to JS. Otherwise, browser blocks access (even though server responded).
        
- So **CORS is not about disabling security** — it’s about **controlled sharing**.

### How CORS Works: A Simplified Look at the Handshake

- The CORS mechanism involves a negotiation between the browser (client) and the server hosting the requested resource.
    
- The browser plays a key role in initiating and enforcing CORS rules.
    
- **The `Origin` Request Header**:
    
    - When a script on a webpage attempts to make a cross-origin request to a resource on a different server, the browser automatically attaches an `Origin` HTTP header to its outgoing request, specifying its scheme, hostname & port.
        
- The server's response headers grant permission.
    
    - After the server receiving the request with an `Origin` header, if it decided to allow the request, the server must include specific CORS headers in its HTTP response.
        
    - The most crucial of these are:
        
        - `Access-Control-Allow-Origin`: `https://www.example.com`
            - ↪️ This explicitly tells the browser that requests from `https://www.example.com` are permitted.
            - ↪️ The server should ideally also include `Origin` with the `Vary` response header if it dynamically returns a specific origin - indicating that the response might differ based on the request `Origin` header.
                
        - `Access-Control-Allow-Origin`: `*`
            - ↪️ Signifies that requests from any origin are permitted.
    

---

## 3) Simple vs. Preflighted Requests

### Simple requests
- Not all cross-origin requests require full CORS negotiation involving a preflight check.

- Sent **without preflight** if ALL these are true:
    - Method is `GET`, `HEAD`, or `POST`.
        
    - Headers are only simple ones: `Accept`, `Accept-Language`, `Content-Language`, `Content-Type` (with value only `text/plain`, `multipart/form-data`, or `application/x-www-form-urlencoded`).
        
    - No custom headers, no `Authorization` header.

### Preflighted requests
- Requests that are not simple are considered more complex & potentially "risky", as they might modify data on the server or use non-standard headers.

- Anything else (e.g., `PUT`, `DELETE`, `PATCH`, custom headers, non-simple `Content-Type`) triggers a **preflight**.
    
- Browser first sends an **`OPTIONS` request** with headers:
    - `Origin`
        
    - `Access-Control-Request-Method`
        
    - `Access-Control-Request-Headers`
        
- Server responds with headers like:
    
    - `Access-Control-Allow-Origin: https://app.com`
        
    - `Access-Control-Allow-Methods: GET, POST, PUT`
        
    - `Access-Control-Allow-Headers: X-Custom-Header`
        
    - `Access-Control-Max-Age: 600` (cache preflight for 10 minutes)
        
- If allowed, browser sends the actual request next.
    

---

## 4) Key CORS response headers

- **`Access-Control-Allow-Origin`** — required. Either a specific origin or `*` (wildcard). Example:

```http
Access-Control-Allow-Origin: https://app.com
```
    
- **`Access-Control-Allow-Methods`** — allowed HTTP methods.
    
- **`Access-Control-Allow-Headers`** — allowed custom headers.
    
- **`Access-Control-Expose-Headers`** — which response headers JS can read (e.g., `X-Total-Count`). Without this, only a safe subset is exposed.
    
- **`Access-Control-Allow-Credentials`** — whether cookies/credentials can be shared. **Must not** be used with `*`.
    
- **`Access-Control-Max-Age`** — cache duration for preflight results.
    

---

## 5) Credentials and CORS

- By default, cross-origin requests don’t send cookies or HTTP auth.
    
- To include them:
    
    - Client: `fetch(url, { credentials: 'include' })`
        
    - Server: `Access-Control-Allow-Credentials: true`
        
    - Server must also reply with a **specific** origin (not `*`).

Example:

```js
// Client
fetch('https://api.app.com/data', { credentials: 'include' });
```

```http
// Server response
Access-Control-Allow-Origin: https://www.app.com
Access-Control-Allow-Credentials: true
```

If these don’t match, browser blocks response.

---

## 6) Common pitfalls

- **Wildcard + credentials** is forbidden:
 ```http
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Credentials: true  # ❌ not allowed
```
    
- Servers must echo back the **exact Origin**.
    
- Preflight cache is per-origin + method + headers. Adding a new custom header can trigger fresh preflights.
    
- Browsers hide blocked response details for security (console shows only generic error).
    

---

## 7) Extended example

### Scenario

Frontend at `https://shop.com` calls API at `https://api.shop.com` with custom header `X-Auth`.

### Flow

1. Browser sends preflight:

```http
OPTIONS /orders HTTP/1.1
Origin: https://shop.com
Access-Control-Request-Method: POST
Access-Control-Request-Headers: X-Auth
```

2. Server replies:
    

```http
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: https://shop.com
Access-Control-Allow-Methods: POST
Access-Control-Allow-Headers: X-Auth
Access-Control-Max-Age: 3600
```

3. Browser now sends actual POST with `X-Auth`.
    

---

## 8) Security perspective

- CORS doesn’t weaken SOP; it gives server owners control.
    
- If misconfigured, CORS can expose sensitive APIs. E.g., allowing `Access-Control-Allow-Origin: *` with `Access-Control-Allow-Credentials: true` would leak user data to any site.
    

---

## 9) Quick reference table

|Situation|Preflight?|Server must reply with|
|---|---|---|
|GET request with no custom headers|No|`Access-Control-Allow-Origin`|
|POST with `Content-Type: application/json`|Yes|`Access-Control-Allow-Origin`, `Access-Control-Allow-Methods`, maybe `Access-Control-Allow-Headers`|
|Request with cookies|Maybe|`Access-Control-Allow-Origin` (specific), `Access-Control-Allow-Credentials: true`|
|Custom header (e.g., `X-API-Key`)|Yes|`Access-Control-Allow-Headers` including that header|

---

## 10) Debugging tips

- Use browser DevTools → **Network** tab → check `OPTIONS` request & response.
    
- Watch console for CORS errors.
    
- Test server headers with `curl -i -X OPTIONS` or `httpie`.
    
- Mock/test with tools like **MSW** (Mock Service Worker) or Postman (though Postman bypasses browser CORS enforcement).
    

---

### TL;DR

- Browser enforces SOP; CORS is the escape hatch for legit cross-site API use.
    
- Simple requests skip preflight; others need OPTIONS.
    
- Always set `Access-Control-Allow-Origin` properly.
    
- For cookies/credentials: both client and server must opt in.
    
- Debug CORS by checking the **preflight response headers**.

---
## References