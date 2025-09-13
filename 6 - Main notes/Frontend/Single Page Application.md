
2025-07-09 15:13

Status:

Tags:

---
# Single Page Application

A Single-Page Application (SPA) is a modern style of web application creation where **the website consists of only one HTML page fetched from the server**. Instead of fetching separate pages from the server for different views or updates, the content of this single page is **dynamulated dynamically using JavaScript that executes in the browser**.

Here's a breakdown of how SPAs work and their key characteristics:

- **Core Principle**: Unlike traditional web applications where the browser fetches a new HTML document from the server for every page navigation or data submission, an SPA loads a single HTML page initially. Subsequent updates to the content are handled by JavaScript running in the browser, which fetches necessary data (often in JSON format) from the server without requiring a full page reload.
- **Contrast with Traditional Web Apps**:
    - In a **traditional web application**, like the homepage of the example application, all application logic resides on the server. The server dynamically forms and sends the HTML document, and the browser's role is primarily to render this HTML. When a form is submitted, the server might respond with a redirect, causing the browser to reload the entire page.
    - In an **SPA**, more responsibility for generating and manipulating HTML code for displaying data is given to the browser. The browser executes JavaScript code that fetches data from the server (e.g., JSON data for notes) and then uses the **Document Object Model (DOM) API** to add or modify HTML elements on the page.
- **How Data Submission Works in an SPA (Example)**:
    - In the example SPA version of the notes app (`https://studies.cs.helsinki.fi/exampleapp/spa`), when a new note is created, the form element has **no `action` or `method` attributes**, which are typically used for traditional form submissions.
    - Instead, **JavaScript code intercepts the form's submit event** by calling `e.preventDefault()`, preventing the browser's default behavior of sending data and causing a full page reload.
    - The JavaScript then **creates a new note object** and immediately **adds it to the local list of notes**, **re-renders the note list on the page**, and **sends the new note to the server**.
    - The note is sent to the server using an **HTTP POST request** (e.g., to `/new_note_spa`), with the **new note's data sent as JSON** in the request body. The `Content-Type` header is set to `application/json` to inform the server about the data format.
    - Crucially, the **server responds with a status code like 201 Created** and **does not instruct the browser to perform a redirect**. The browser remains on the same page, avoiding further HTTP requests for page assets.
- **Role of AJAX and `XMLHttpRequest`**:
    - The concept behind SPAs heavily relies on **AJAX (Asynchronous JavaScript and XML)**, a term introduced to describe fetching content to web pages using JavaScript without needing to re-render the page.
    - **`XMLHttpRequest` (XHR)** is a built-in JavaScript object that was one of the first tools enabling AJAX requests. It allows web pages to make HTTP requests to a server in the background without reloading the entire page. Although more modern alternatives like `fetch()` are now common, XHR is still supported and demonstrates the underlying mechanism.
    - For instance, in the example, `XMLHttpRequest` is used to send the new note as JSON data to the server in the SPA version.
- **Development with Libraries**: While the example app uses "vanilla JavaScript" and the DOM-API for page manipulation, modern SPAs often utilize JavaScript libraries and frameworks to simplify development. Historically, jQuery, BackboneJS, and AngularJS were popular. Currently, **Facebook's React library** is widely used for implementing browser-side logic in web applications, often alongside libraries like Redux. VueJS is also a newer, emerging alternative.

---
## References
[XMLHttpRequest() - grandfather of AJAX](Javascript%20notes/XMLHttpRequest()%20-%20grandfather%20of%20AJAX.md)
