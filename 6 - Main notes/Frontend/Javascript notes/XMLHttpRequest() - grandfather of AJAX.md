
2025-07-08 18:51

Status:

Tags:

---
# XMLHttpRequest() - grandfather of AJAX

Great! Let's break down `XMLHttpRequest()` in simple terms — especially if you're learning JavaScript or working on frontend web development.

---

## 🧠 What is `XMLHttpRequest()`?

`XMLHttpRequest` (often abbreviated as **XHR**) is a **built-in JavaScript object** that allows web pages to make **HTTP requests** to a server **without reloading** the page.

> ✅ It was one of the first tools for making AJAX (Asynchronous JavaScript and XML) requests.

---

## 🎯 What Problem Does It Solve?

Imagine you're filling out a form, and you want to:
- check if a username is available
- submit part of the form without refreshing the whole page

Before `XMLHttpRequest`, you'd have to reload the entire page — slow and annoying. XHR lets you do that in the background!

---

## 🛠 How It Works (Basic Example)

```javascript
// 1. Create the request
const xhr = new XMLHttpRequest();

// 2. Setup the request: GET request to a URL
xhr.open("GET", "https://jsonplaceholder.typicode.com/posts/1", true);

// 3. Define what to do when response comes back
xhr.onload = function () {
  if (xhr.status === 200) {
    console.log("Response:", xhr.responseText);
  } else {
    console.error("Error:", xhr.status);
  }
};

// 4. Send the request
xhr.send();
```

---

## ⚙️ Key Methods and Properties

| Method/Property     | Purpose                                       |
|---------------------|-----------------------------------------------|
| `.open(method, url, async)` | Sets up the request method & URL         |
| `.send()`           | Sends the request to the server               |
| `.onload`           | Triggered when the response is received       |
| `.status`           | HTTP status code (e.g., 200 OK, 404 Not Found)|
| `.responseText`     | The raw response as text                      |

---

## 🚀 Modern Alternative: `fetch()`

`XMLHttpRequest` is older and more verbose. Today, we often use `fetch()`:

```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then(response => response.json())
  .then(data => console.log(data));
```

But `XMLHttpRequest` is still supported in all browsers and useful for learning and legacy apps.

---

## ✅ Key Takeaway

`XMLHttpRequest()` is the **grandfather of AJAX**, letting JavaScript talk to servers without refreshing the page — useful for dynamic web experiences.



---
## References

[onreadystatechange - XMLHttpRequest() event handler]()%20event%20handler)%20event%20handler.md)