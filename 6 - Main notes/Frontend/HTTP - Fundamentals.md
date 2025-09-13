
2025-07-09 13:21

Status:

Tags: [Networking](../../3%20-%20Tags/Networking.md)

---
# HTTP - Fundamentals
[HTTP Fundamentals](https://dev.to/temiogundeji/http-the-fundamentals-339c)

**In-depth Notes: "HTTP: The Fundamentals" by Temi Ogundeji**

### **1. Introduction to HTTP**

- HTTP stands for **HyperText Transfer Protocol**.
- It's the foundation of data communication for the web.
- Enables communication between clients (e.g., browsers) and servers.
- Uses a **request-response model**.
- HTTP (Hypertext Transfer Protocol) exhibits several key characteristics:
	- Stateless: It is stateless, so it doesn't keep track of past requests or sessions. **The server also doesn't store client-specific information between requests**. Cookies and session tokens are used to maintain the state instead.
	- Connectionless: It is connectionless. Each request-response exchange is a separate transaction, and **once the response is delivered, the client-server connection is closed**. This allows for efficient resource allocation on servers.
	    
	- Text-Based: It is a text-based protocol, where messages exchanged between clients and servers are in human-readable format. **Both requests and responses consist of plain text lines containing headers, status codes, and optional message bodies.** This text-based nature makes it easy to read and debug HTTP traffic.
	    
	- Extensible: It is an extensible protocol, allowing for the **development of additional features and protocols built upon its foundation**. It supports the addition of custom headers, methods, and protocols to cater to specific requirements or enhance functionality. This extensibility has facilitated the growth of web technologies and APIs built on top of HTTP.
	    
	- Flexible Content Handling: It can handle various types of content, including HTML pages, images, documents, videos, and more. It supports content negotiation, allowing clients and servers to agree on the most appropriate representation of a resource based on factors such as content type, language, or encoding.
	    
	- Uniform Resource Identification: Uses Uniform Resource Identifiers (URIs) to identify and locate web resources. URIs (It identifies a resource and differentiates it from others by using a name, location, or both.) specify the address and path to a specific resource on the web. They provide a standardized way to reference and access resources across different web platforms.
	    
	- Scalability: It is designed to be scalable, allowing for a large number of clients to interact with servers concurrently. It supports parallel processing of multiple requests and responses, enabling efficient handling of high-traffic loads.
	    
	- Caching: It includes mechanisms for caching resources, allowing clients to store copies of resources locally. Caching reduces the need for repeated requests to the server, thereby improving the performance of web applications and reducing network traffic.
    

### **2. HTTP Methods**

- HTTP defines several methods that indicate the desired action to be performed for a given resource:
    
    - **GET**: Retrieve data.
	    - The GET method is used to retrieve data from the server without any changes to it.
	    - It is also preferred over the POST method as it can be addressed over the URL [^1]
	    - **Example** use-cases for GET requests are: Getting the list of blog posts by a particular author in a blog app. Getting the list of products added to the shopping cart by a user.
        
    - **POST**: Submit data to be processed.
	    - POST method is used when sending data to the server.
	    - Some of its use cases are file upload, form submission and so on. Every time you post a message to a forum, subscribe to a mailing list or complete an online shopping transaction. You make use of the POST method.
        
    - **PUT**: Update/replace existing data.
	    - The PUT method asks the target resource to establish or modify its state according to the representation provided in the request.
	    - The client defines the server's target location, which sets it apart from POST. 
	    - Also, it is used to update an existing resource on the server. 
	    - It is typically used when the client wants to send data to the server to replace or modify an existing resource. 
	    - If you retry a request numerous times, that will be equal to a single request conversion i.e. It is idempotent.
        
    - **PATCH**: Apply partial updates.
	    - The PATCH method makes partial modification to a target resource. It does this without completely replacing the resource.
        
    - **DELETE**: Remove a resource.
        
    - **OPTIONS**: Describe communication options for the resource.
        
    - **HEAD**: Similar to GET but only returns headers.        

### **3. Structure of an HTTP Requests and Responses**
HTTP works through a mechanism called HTTP messages. There are two types of HTTP messages:
```
- Request: They are messages sent by clients to the server to trigger an action.
- Response: They are messages sent to the client by the server in response to the request made by the client.
```
![Pasted image 20250709142141](../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250709142141.png)

- An HTTP request is composed of:    
    - **Request Line**: Contains the method, URI, and HTTP version (e.g., `GET /index.html HTTP/1.1`).
    - **Headers**: Key-value pairs that carry metadata (e.g., `Content-Type`, `Authorization`).
    - **Body**: Optional, used mainly in POST/PUT for carrying data (e.g., form inputs, JSON
    - A set of header fields are simply metadata sent with a request to provide information about the request. Each header is specified using this format.

		`Host: en.wikipedia.com.`
		
		`Connection: Keep-Alive.`

- The two examples (Host and Connection) above are some of the important request headers that should be used in our HTTP requests. Also, we can introduce our headers too.
- Request Headers are used in HTTP requests to provide information about the HTTP requests so that the server can tailor the response accordingly. Headers are specific in their functions. For example, 
	- there is a header whose function is to supply authentication credentials.
	- Also, Accept-* headers are used to specify the format of the response acceptable by the client. 
	- Other functions of headers are to control caching, 
	- get information about the user-agent or referrer etc. 
- Note, some headers exist in the request header but are referred to as **representation headers** by the specification. An example is the popular Content-Type header.'
```
GET /about.html HTTP/1.1
Host: [https://www.freecodecamp.org/news/about/](https://www.freecodecamp.org/news/about/)
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html, application/xhtml+xml,application/xml;q=0.9,_/_;q=0.8\
Accept-Language: en-US, en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: [https://www.freecodecamp.org/news](https://www.freecodecamp.org/news)
Connection: keep-alive
Upgrade-Insecure-Requests: 1
If-Modified-Since: Mon, 18 Jul 2016 02:36:04 GMT
If-None-Match: "c561c68d0ba92bbeb8b0fff2a9199f722e3a621a"
Cache-Control: max-age=0
```

### **Structure of an HTTP Response**
- Composed of:    
    - **Status Line**: HTTP version, status code (e.g., 200 OK).
    - **Headers**: Metadata (e.g., `Content-Length`, `Content-Type`).
    - **Body**: Actual content like HTML, JSON, etc.
- The response header is a component of a network packet sent by a server to a client in response to the request sent by the client. It is utilized in web communication to deliver web pages and other resources to clients. The information embedded with the HTTP response header includes the destination IP address, data type, host address and more. 
- The HTTP response body is the data that is sent from a server to a client as part of an HTTP response. It contains the content or payload that the client requested from the server. The response body can include various types of data, such as HTML, XML, JSON, images, videos, or plain text.


**5. HTTP Status Codes**
- Status codes provide information about the outcome of the request:
    
    - **1xx (Informational)**: Request received, continuing process.
        
    - **2xx (Success)**:
	    - This indicates that the request made by the client to the server has been successful. Or that the server returned the right response to the client’s request. A successful response can have different meanings depending on the type of request method used. For example: for the GET request method: It means that the client has successfully fetched the requested resources from the server, for the POST method, it could mean that a resource password to the request body has been stored on the server in the DB.
        - 200 OK: Standard success.
        - 201 Created: Resource created.
            
    - **3xx (Redirection)**:
        - 301 Moved Permanently
        - 302 Found (temporary redirection)
        - The HTTP redirection error messages are the responses that are given by the server side to guide the client to a new location by providing the URL of that specific place. These codes are returned if the request has more than one possible response.
            
    - **4xx (Client Error)**:
        - 400 Bad Request
        - 401 Unauthorized
        - 403 Forbidden
        - 404 Not Found
        - These are error messages that occur as a result of a client's request. It means the request contains incorrect syntax or cannot be fulfilled. It could be that the user sent too many requests in a lesser amount of time which is not in line with the server’s rate-limiting configuration, It could be as a result of the client not authenticating and many other reasons. The client error code returned by the server indicates the cause of the error.
            
    - **5xx (Server Error)**:
        - 500 Internal Server Error
        - 503 Service Unavailable
        - Server error codes are also considered errors. However, they denote that the problem is on the server’s end. This can make them more difficult to resolve.
            

### **6. Statelessness of HTTP**
- HTTP is **stateless**:
    - Each request is **independent** and doesn’t retain information from previous requests.
    - This design improves scalability and simplicity.        

### **7. Cookies and Sessions**
- To overcome statelessness, web applications use:
    - **Cookies**: Small pieces of data stored on the client-side.
    - **Sessions**: Server-side storage that uses a session ID (often sent via cookies).

### **8. HTTPS: Secure HTTP**
- **HTTPS** = HTTP + **SSL/TLS** encryption.
- Ensures:
    - **Confidentiality**: Prevents eavesdropping.
    - **Integrity**: Data is not altered in transit.
    - **Authentication**: Confirms the server's identity using digital certificates.       

### **9. REST and HTTP**
- REST (Representational State Transfer) is an architectural style that often uses HTTP.
- Core principles of REST align well with HTTP methods:
    - Use appropriate HTTP methods.
    - Resources are identified using URIs.
    - Stateless communication.
        

### **10. Conclusion**

- Understanding HTTP is crucial for all web developers.
    
- It's the backbone of any interaction on the internet.
    
- Knowing the request-response flow, status codes, and HTTP methods enhances debugging and API design skills.


Explanation:

When using the **GET** method, data is **appended to the URL** as query parameters. For example:

```
GET /search?query=books&page=2 HTTP/1.1
```

This makes the request:
- **Easily shareable** (you can copy and paste the URL).
- **Bookmarkable** (browsers can save the exact request).
- **Cacheable** (browsers and proxies can cache the response).
In contrast, the **POST** method:
- Sends data in the **body** of the request, **not visible in the URL**.
- Is typically used for sensitive or larger payloads.
- Is **not cacheable** and **cannot be bookmarked or shared easily**.
    
**Why GET might be preferred**:
For operations like searching, filtering, or any action that **doesn’t modify data on the server**, **GET is preferred** because:
- It's simpler,
- It's REST-compliant (safe and idempotent),
- And it can be **"addressed over the URL"**, meaning the request and its parameters are visible and accessible through the address bar.



---

## References
 [^1]: [Why GET is preferred over the POST method](Why%20GET%20is%20preferred%20over%20the%20POST%20method.md)
