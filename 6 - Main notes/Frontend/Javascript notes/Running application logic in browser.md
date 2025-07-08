
2025-07-08 16:30

Status:

Tags:

---
# Running application logic in the browser
When application logic runs in the browser, it generally involves the following steps:

- **Initial Document Fetch**: The browser first sends an **HTTP GET request** to a server to retrieve the base HTML document for the page.
- **Resource Loading**: This initial HTML document typically contains `<script>` and `<link>` tags that instruct the browser to make further **HTTP GET requests** to fetch associated resources, such as JavaScript files (e.g., `main.js`) and CSS stylesheets (e.g., `main.css`).
- **JavaScript Execution**: Once the JavaScript file is fetched, the browser begins to **execute the JavaScript code** within it.
- **Asynchronous Data Fetching**: This running JavaScript code then often initiates **additional HTTP GET requests** to the server to fetch application-specific data, commonly in **JSON format** (e.g., from `/data.json`). This is done using mechanisms like `XMLHttpRequest` (or `fetch` in modern applications), which allows fetching content without requiring the entire page to reload.
- **Client-Side Rendering (DOM Manipulation)**: Upon receiving the data (e.g., JSON notes data), the JavaScript code executes an **event handler** (a callback function). This function processes the fetched data and **dynamically constructs or modifies HTML elements** on the page. This is achieved by using the **Document Object Model (DOM) API**, which provides an interface for programmatically altering the web page's element tree. For example, new list items might be created and appended to an existing list structure.
- **Styling with CSS**: The fetched CSS stylesheet defines **Cascading Style Sheets (CSS)** rules, which are then applied by the browser to determine the appearance and layout of the HTML elements, including those dynamically created by JavaScript.
- **Client-Side Changes are Temporary**: It's important to understand that any changes made to the page through client-side JavaScript and the DOM-API are **not permanent**. If the page is reloaded, these changes will disappear, as the browser will re-render the page based on the original HTML and data fetched from the server. For changes to persist, they must be sent back to the server, typically via a separate mechanism like an HTTP POST request.

This approach allows the browser to take on more responsibility for rendering and manipulating page content, moving away from the "dumb" browser model of traditional web applications where all logic and data presentation originated solely from server-generated HTML. This shift was significantly influenced by the advent of **AJAX** around 2005.

### Explained with exampl
The "Running application logic in the browser" section, as described in the sources, signifies a departure from traditional web application models where the browser is "dumb" and all logic resides on the server. In this approach, **the browser takes on more responsibility for generating and manipulating the page content**, primarily through the execution of JavaScript code.

Here's a breakdown of how application logic runs in the browser, using the example of the `https://studies.cs.helsinki.fi/exampleapp/notes` page:

- **Initial Page Load and Resource Fetching**:
    
    - When you navigate to `https://studies.cs.helsinki.fi/exampleapp/notes`, the browser first sends an **HTTP GET request to the server to fetch the HTML code** of the page.
    - The HTML code returned by the server for the notes page does _not_ initially contain the list of notes itself. Instead, its `head` section includes a `<script>` tag that instructs the browser to **fetch a JavaScript file**, specifically `main.js`, and also a CSS stylesheet `main.css`. These are also fetched via **HTTP GET requests**.
- **JavaScript Execution and Data Fetching**:
    
    - Immediately after fetching the `main.js` script, **the browser begins to execute the JavaScript code** contained within it.
    - This JavaScript code then initiates **another HTTP GET request** to the server, specifically to the address `https://studies.cs.helsinki.fi/exampleapp/data.json`. This request is made using `XMLHttpRequest` in the example, which is an older method, though modern applications typically use `fetch` (which will be covered later in the course).
    - The response from `data.json` is **raw JSON data** containing the notes.
- **Client-Side Rendering and DOM Manipulation**:
    
    - Once the JSON data is fetched from the server, the JavaScript code executes an **event handler (a callback function)** that processes this data.
    - This code **parses the JSON data** and then **dynamically forms an unordered bullet-point list** (`<ul>`) of notes.
    - It does this by using the **Document Object Model (DOM) API** to create new HTML elements (`<li>` tags for each note) and append them to the appropriate place in the existing HTML tree of the page. For example, `document.createElement('ul')` creates a new unordered list element, and `ul.appendChild(li)` adds list items to it.
    - Only the `content` field of each note from the JSON data is used for rendering; timestamps are ignored.
- **Role of CSS and Developer Console**:
    
    - The fetched `main.css` file contains **Cascading Style Sheets (CSS)** rules that determine the appearance of web pages. For instance, it defines styles for elements with `container` and `notes` classes, like setting a border or text color.
    - The **Developer Console's _Network_ tab** is essential for observing these HTTP GET requests and responses. The _Response_ tab shows the actual data returned, while the _Elements_ tab allows inspection and temporary modification of the DOM and CSS attributes. The _Console_ tab displays `console.log` outputs from the JavaScript code.
- **Non-Permanent Changes**: It's important to note that any changes made to the page directly in the browser (e.g., through the console using DOM-API) are **not permanent**. If the page is reloaded, these changes will disappear because the page will be re-rendered based on the original HTML and JSON data fetched from the server. For changes to be permanent, they must be pushed to the server.
    

This approach, exemplified by the notes page, started to incorporate concepts like **AJAX** (Asynchronous JavaScript and XML), which enabled fetching content to web pages using JavaScript without needing to re-render the entire page, a revolutionary concept around 2005. This contrasts with **traditional web applications** where _all_ displayed data was fetched as part of the HTML code generated by the server.

- The last two lines instruct the browser to do an HTTP GET request to the server's address _/data.json_:

```js
xhttp.open('GET', '/data.json', true)
xhttp.send()
```

This is the bottom-most request shown on the Network tab.

We can try going to the address [https://studies.cs.helsinki.fi/exampleapp/data.json](https://studies.cs.helsinki.fi/exampleapp/data.json) straight from the browser:

![Raw JSON Data](https://fullstackopen.com/static/cb83e4c1c89fd4bc662942457f30403e/5a190/10e.png)

---
## References