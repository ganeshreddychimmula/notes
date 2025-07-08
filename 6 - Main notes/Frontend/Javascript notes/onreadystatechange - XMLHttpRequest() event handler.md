
2025-07-08 18:52

Status:

Tags:

---
# onreadystatechange - XMLHttpRequest() event handler
Let’s dive into `onreadystatechange` — one of the most important event handlers when working with `XMLHttpRequest`.

---

## 🧠 What is `onreadystatechange`?

`onreadystatechange` is an **event handler** property of the `XMLHttpRequest` object.  
It’s triggered **every time the ready state of the request changes** (i.e., as it moves through different stages of the HTTP request-response lifecycle).

---

## 🔁 What are the Ready States?

`XMLHttpRequest.readyState` can have **five values**:

|Value|State|Description|
|---|---|---|
|0|`UNSENT`|Request created, but `open()` not called yet|
|1|`OPENED`|`open()` has been called|
|2|`HEADERS_RECEIVED`|`send()` has been called; headers received|
|3|`LOADING`|Response is being downloaded (in progress)|
|4|`DONE`|Request finished and response is ready|

---

## 🧪 Basic Example:

```javascript
const xhr = new XMLHttpRequest();
xhr.open("GET", "https://jsonplaceholder.typicode.com/posts/1", true);

xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status === 200) {
    console.log("Success:", xhr.responseText);
  }
};

xhr.send();
```

### 🔍 Explanation:

- The function inside `onreadystatechange` will run **multiple times** (each time the ready state changes).
    
- We usually check:
    
    ```js
    if (xhr.readyState === 4 && xhr.status === 200)
    ```
    
    to ensure that:
    
    - the request is fully completed (`readyState === 4`)
        
    - the response was successful (`status === 200`)
        

---

## ✅ When to Use It vs. `onload`

|Feature|`onreadystatechange`|`onload`|
|---|---|---|
|More verbose|Yes (fires multiple times)|No (fires once when done)|
|Backward compatible|✅ Yes (older browsers too)|❌ No (newer browsers only)|
|Used for:|Fine control over each request stage|Simpler response handling|

---

## 🧠 Key Takeaway

`onreadystatechange` lets you **track every phase** of a request.  
In modern code, you often just wait for `readyState === 4`, but knowing the full lifecycle helps when debugging or dealing with older APIs.

Would you like a full example with `POST` or showing a loading spinner at `readyState === 3`?

---
## References