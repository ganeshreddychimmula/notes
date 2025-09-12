
2025-07-08 13:37

Status:

Tags:

---
# 0 b Fundamentals of Web apps - Fullstackopen

- 1st rule of web development: Always keep the developer console open on your web browser.
- To open developer console - F^12
- Remember to _always_ keep the Developer Console open when developing web applications.
- Make sure that the _Network_ tab is open, and check the _Disable cache_ option as shown. _Preserve log_ can also be useful (it saves the logs printed by the application when the page is reloaded) as well as "Hide extension URLs"(hides requests of any extensions installed in the browser)).

### HTTP GET
[Example App](https://studies.cs.helsinki.fi/exampleapp/)
- **HTTP GET is the method used for communication between the server and the web browser, following the HTTP protocol**.
- The **Developer Console's _Network_ tab** is crucial for observing how the browser and server communicate using HTTP.
- When you reload a web page, the console typically shows **two main HTTP GET events**:
    1. The browser fetches the contents of the page (e.g., `https://studies.cs.helsinki.fi/exampleapp`) from the server.
    2. The browser downloads associated images, such as `kuva.png`.
![Pasted image 20250708152526](../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250708152526.png)
- **Request Details (for page content)**:
    - The browser uses the **GET method** to request the address.
    - A **Status code 200** indicates that the request was successful.
    - **Response headers** provide information like the size of the response in bytes and the exact response time.
    ```json
	HTTP/1.1 200 OK server: nginx/1.20.1 date: Tue, 08 Jul 2025 18:54:46 GMT content-type: text/html; charset=utf-8 content-length: 321 x-powered-by: Express etag: W/"141-T/danxJCVua08jxAk4P+sdtBvQY
	```
    - An important header, ==**Content-Type**==, specifies that the response is a text file in UTF-8 format, formatted with HTML (e.g., `text/html; charset=utf-8`). This helps the browser render it as a web page.
    - The **Response tab** shows the actual HTML data returned by the server. The `body` section within this HTML determines the structure of what is rendered on the screen.

- **Request Details (for images)**:
    - Because an `img` tag is present in the HTML, the browser performs a **second HTTP GET request** to fetch the image (e.g., `kuva.png`) from the server.
    - This request is made to the image's specific address (e.g., `https://studies.cs.helsinki.fi/exampleapp/kuva.png`).
    - The response headers for the image tell the browser its size (e.g., 89350 bytes) and its **Content-type** (e.g., `image/png`), enabling correct rendering of the image.
![7m](../../2%20-%20Source%20Material/Media%20and%20other%20files/7m.png)
- **Sequence of Events**:
    - A sequence diagram visually represents the communication flow, with time moving from top to bottom.
    - Initially, the browser sends an **HTTP GET request for the HTML code of the page**.
    - The `img` tag within the received HTML then prompts the browser to **fetch the image (`kuva.png`) via another HTTP GET request**.
    - The HTML page starts rendering even _before_ the image has been fully fetched from the server.
- **JavaScript and HTTP GET**:
    - In more dynamic applications, JavaScript code can initiate HTTP GET requests.
    - The example notes page uses **`XMLHttpRequest`** (an older method, but the course will cover modern `fetch` later) to send an HTTP GET request to `/data.json`.
    - Accessing `https://studies.cs.helsinki.fi/exampleapp/data.json` directly in the browser reveals **notes in raw JSON data format**.
    - The JavaScript code on the notes page **downloads this JSON data** containing the notes.
    - When a page like `https://studies.cs.helsinki.fi/exampleapp/notes` is opened, the browser first fetches the HTML code, then the CSS style sheet (`main.css`), and then the JavaScript code file (`main.js`), all using **HTTP GET requests**.
    - The executed JavaScript then makes another **HTTP GET request to fetch the JSON notes data**.
### Traditional Web Applications
Traditional or **old-school web applications** operate on a principle where the **browser is considered "dumb"** and primarily fetches HTML data from the server. In this model, **all application logic resides on the server**. [^2]

The example uses [Express](https://expressjs.com/) library with Node.js. This course will use Node.js and Express to create web servers.

### Running application logic in the browser [^4]
[Example used](https://studies.cs.helsinki.fi/exampleapp/notes)
When application logic runs in the browser, it generally involves the following steps:

- **Initial Document Fetch**: The browser first sends an **HTTP GET request** to a server to retrieve the base HTML document for the page.
- **Resource Loading**: This initial HTML document typically contains `<script>` and `<link>` tags that instruct the browser to make further **HTTP GET requests** to fetch associated resources, such as JavaScript files (e.g., `main.js`) and CSS stylesheets (e.g., `main.css`).
- **JavaScript Execution**: Once the JavaScript file is fetched, the browser begins to **execute the JavaScript code** within it.
- **Asynchronous Data Fetching**: This running JavaScript code then often initiates **additional HTTP GET requests** to the server to fetch application-specific data, commonly in **JSON format** (e.g., from `/data.json`). This is done using mechanisms like `XMLHttpRequest` (or `fetch` in modern applications), which allows fetching content without requiring the entire page to reload. [^3]
- **Client-Side Rendering (DOM Manipulation)**: Upon receiving the data (e.g., JSON notes data), the JavaScript code executes an **event handler** (a callback function). This function processes the fetched data and **dynamically constructs or modifies HTML elements** on the page. This is achieved by using the **Document Object Model (DOM) API**, which provides an interface for programmatically altering the web page's element tree. For example, new list items might be created and appended to an existing list structure.
- **Styling with CSS**: The fetched CSS stylesheet defines **Cascading Style Sheets (CSS)** rules, which are then applied by the browser to determine the appearance and layout of the HTML elements, including those dynamically created by JavaScript.
- **Client-Side Changes are Temporary**: It's important to understand that any changes made to the page through client-side JavaScript and the DOM-API are **not permanent**. If the page is reloaded, these changes will disappear, as the browser will re-render the page based on the original HTML and data fetched from the server. For changes to persist, they must be sent back to the server, typically via a separate mechanism like an HTTP POST request.

This approach allows the browser to take on more responsibility for rendering and manipulating page content, moving away from the "dumb" browser model of traditional web applications where all logic and data presentation originated solely from server-generated HTML. This shift was significantly influenced by the advent of **AJAX** around 2005.

-  [^4]: The last two lines instruct the browser to do an HTTP GET request to the server's address _/data.json_:

```js
xhttp.open('GET', '/data.json', true)
xhttp.send()
```

This is the bottom-most request shown on the Network tab.

We can try going to the address [https://studies.cs.helsinki.fi/exampleapp/data.json](https://studies.cs.helsinki.fi/exampleapp/data.json) straight from the browser:

![Raw JSON Data](https://fullstackopen.com/static/cb83e4c1c89fd4bc662942457f30403e/5a190/10e.png)

### Event handlers and Callback functions 

Here are notes for the "Event handlers and Callback functions" section, drawing directly from the sources:

- **Definition of an Event Handler**: An event handler is a **function defined for an object**. When a specific event associated with that object occurs, the **browser calls this event handler function**.
- **Callback Functions**: Event handler functions are also known as **callback functions**. This term emphasizes that the **application code does not invoke these functions itself**. Instead, the **runtime environment (the browser) invokes the function at an appropriate time** when the event has occurred.
- **Example (`xhttp.onreadystatechange`)**: [^5] [^6]
    - In the provided code, an `onreadystatechange` event handler is defined for the `xhttp` object, which is used for making HTTP requests.
    - The `xhttp.send()` command sends the request to the server, but the code to handle the response is defined further up, within this event handler.
    - The browser invokes this function **whenever the state of the `xhttp` object changes**.
    - Inside this callback function, the code typically **checks that the `readyState` equals 4** (meaning "The operation is complete") **and that the HTTP status code of the response is 200** (indicating success) before processing the server's response.
- **Commonality**: This mechanism of invoking event handlers is **very common in JavaScript** for handling asynchronous operations (like network requests) and user interactions.

### Document Object Model or DOM [^7]
The functioning of the browser is based on the idea of depicting HTML elements as a tree.

Document Object Model, or [DOM](https://en.wikipedia.org/wiki/Document_Object_Model), is an Application Programming Interface (_API_) that enables programmatic modification of the _element trees_ corresponding to web pages.

The JavaScript code introduced in the previous chapter used the DOM-API to add a list of notes to the page.

### Manipulating the document object from console[^7]
The topmost node of the DOM tree of an HTML document is called the _document_ object. We can perform various operations on a webpage using the DOM-API. You can access the _document_ object by typing _document_ into the Console tab:

### CSS
The _head_ element of the HTML code of the Notes page contains a [link](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link) tag, which determines that the browser must fetch a [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) style sheet from the address [main.css](https://studies.cs.helsinki.fi/exampleapp/main.css).

### Loading a page containing JavaScript - review
Let's review what happens when the page [https://studies.cs.helsinki.fi/exampleapp/notes](https://studies.cs.helsinki.fi/exampleapp/notes) is opened on the browser.

![sequence diagram of browser/server interaction](https://fullstackopen.com/static/15a8e6a030a5d6b3d2b4b459c3f2f10f/5a190/19m.png)

- The browser fetches the HTML code defining the content and the structure of the page from the server using an HTTP GET request.
- Links in the HTML code cause the browser to also fetch the CSS style sheet _main.css_...
- ...and the JavaScript code file _main.js_
- The browser executes the JavaScript code. The code makes an HTTP GET request to the address [https://studies.cs.helsinki.fi/exampleapp/data.json](https://studies.cs.helsinki.fi/exampleapp/data.json), which returns the notes as JSON data.
- When the data has been fetched, the browser executes an _event handler_, which renders the notes to the page using the DOM-API

### Forms and HTTP POST [^8]
- When the button on the form is clicked, the browser will send the user input to the server.
- Surprisingly, submitting the form causes no fewer than _five_ HTTP requests. The first one is the form submit event.
- ![Detailed view of the first request](https://fullstackopen.com/static/ac09c143991ad160bdaa1c1381d93f7b/5a190/22e.png)
- It is an [HTTP POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) request to the server address _new_note_. The server responds with HTTP status code 302. This is a [URL redirect](https://en.wikipedia.org/wiki/URL_redirection), with which the server asks the browser to perform a new HTTP GET request to the address defined in the header's _Location_ - the address _notes_.
- So, the browser reloads the Notes page. The reload causes three more HTTP requests: fetching the style sheet (main.css), the JavaScript code (main.js), and the raw data of the notes (data.json).
- The Form tag has attributes _action_ and _method_, which define that submitting the form is done as an HTTP POST request to the address _new_note_.

![action and method highlight](https://fullstackopen.com/static/9463d1dca4170015c47e79065ff98820/5a190/24e.png)
- The code on the server responsible for the POST request is quite simple (NB: this code is on the server, and not on the JavaScript code fetched by the browser):

```js
app.post('/new_note', (req, res) => {
  notes.push({
    content: req.body.note,
    date: new Date(),
  })

  return res.redirect('/notes')
})
```
- Data is sent as the [body](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) of the POST request.
- The server does not save new notes to a database, so new notes disappear when the server is restarted.

### AJAX
[AJAX](https://en.wikipedia.org/wiki/Ajax_\(programming\)) (Asynchronous JavaScript and XML) is a term introduced in February 2005 on the back of advancements in browser technology to describe a new revolutionary approach that enabled the fetching of content to web pages using JavaScript included within the HTML, without the need to rerender the page.

Before the AJAX era, all web pages worked like the traditional web application.

The application URLs reflect the old, carefree times. JSON data is fetched from the URL [https://studies.cs.helsinki.fi/exampleapp/data.json](https://studies.cs.helsinki.fi/exampleapp/data.json) and new notes are sent to the URL [https://studies.cs.helsinki.fi/exampleapp/new_note](https://studies.cs.helsinki.fi/exampleapp/new_note). Nowadays URLs like these would not be considered acceptable, as they don't follow the generally acknowledged conventions of [](https://en.wikipedia.org/wiki/Representational_state_transfer#Applied_to_web_services) APIs, which we'll look into more in [part 3](https://fullstackopen.com/en/part3).
- AJAX, has become so deeply integrated into modern web applications that its underlying principles are now standard, while the original term itself is no longer commonly used

### Single page app[^9]
In recent years, the [Single-page application](https://en.wikipedia.org/wiki/Single-page_application) (SPA) style of creating web applications has emerged. SPA-style websites don't fetch all of their pages separately from the server like our sample application does, but instead comprise only one HTML page fetched from the server, the contents of which are manipulated with JavaScript that executes in the browser

### JavaScript-libraries
Instead of using JavaScript and the DOM-API only, different libraries containing tools that are easier to work with compared to the DOM-API are often used to manipulate pages. One of these libraries is the ever-so-popular [jQuery](https://jquery.com/).
- One of the reasons for the success of jQuery was its so-called cross-browser compatibility. The library worked regardless of the browser or the company that made it, so there was no need for browser-specific solutions. Nowadays using jQuery is not as justified given the advancement of JavaScript, and the most popular browsers generally support basic functionalities well.
- The rise of the single-page app brought several more "modern" ways of web development than jQuery. The favorite of the first wave of developers was [BackboneJS](http://backbonejs.org/). After its [](https://github.com/angular/angular.js/blob/master/CHANGELOG.md#100rc1-moiré-vision-2012-03-13) in 2012, Google's [AngularJS](https://angularjs.org/) quickly became almost the de facto standard of modern web development.
- However, the popularity of Angular plummeted in October 2014 after the [Angular team announced that support for version 1 will end](https://web.archive.org/web/20151208002550/https://jaxenter.com/angular-2-0-announcement-backfires-112127.html), and that Angular 2 will not be backwards compatible with the first version. Angular 2 and the newer versions have not received too warm of a welcome.
- Currently, the most popular tool for implementing the browser-side logic of web applications is Facebook's [React](https://react.dev/) library.
- The status of React seems strong, but the world of JavaScript is ever-changing. For example, recently a newcomer - [VueJS](https://vuejs.org/) - has been capturing some interest.

### Full-stack web development [^10]
We will code the backend with JavaScript, using the [Node.js](https://nodejs.org/en/) runtime environment. Using the same programming language on multiple layers of the stack gives full-stack web development a whole new dimension. However, it's not a requirement of full-stack web development to use the same programming language (JavaScript) for all layers of the stack.

Oftentimes, full-stack developers must also have enough configuration and administration skills to operate their applications, for example, in the cloud.



---
## References
[^2](Javascript%20notes/Traditional%20or%20Old%20school%20web%20applications.md)
[^3](Javascript%20notes/Running%20application%20logic%20in%20browser.md)
[^5]()%20-%20grandfather%20of%20AJAX)%20-%20grandfather%20of%20AJAX.md)
[^6]()%20event%20handler)%20event%20handler.md)
[^7](Javascript%20notes/What%20is%20DOM,%20structure%20and%20navigation%20-%20Javascript.md)
[^8](HTTP%20-%20Fundamentals.md)
[^9](Single%20Page%20Application.md)
[^10](Javascript%20notes/What%20does%20Full%20Stack%20Web%20development%20mean.md)