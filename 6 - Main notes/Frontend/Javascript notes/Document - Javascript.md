
2025-07-08 19:04

Status:

Tags: [JavaScript](../../../3%20-%20Tags/JavaScript.md)

---
# Document - Javascript
### Document

- Manipulating a webpage using JavaScript.
    
- A platform can be a browser, web server, or another host that can run JavaScript.
    
    - Each platform provides platform-specific functionality.
        
    - The JavaScript specification defines a "host environment."
        
    - A host environment provides its own objects and functions in addition to the language core.
        
    - **Example:** Web browsers provide a means to control web pages. Node.js provides server-side features.
        

### Window (Root Object)

1. Global object for JavaScript code.
    
2. Represents the "browser window" and provides methods to control it.
    
3. Automatically created in every browser environment.
    
4. All global variables and functions become properties of `window`.
    

### DOM (Document Object Model) [^1]

- The Document Object Model represents all page content as objects that can be modified.
    
- `document` → main entry point to the page.
    
    - Can create or change anything on the page.
        
- The DOM specification explains the structure of a document and provides objects to manipulate it.
    
- There are non-browser environments that use DOM too.
    

### CSSOM (CSS Object Model)

- The CSS Object Model is the CSS counterpart to the DOM.
    
- Just like DOM represents the HTML structure, CSSOM represents the CSS styles applied to the document, and allows JS to read and modify CSS dynamically.
    
- The CSSOM is the structure created by the browser from the CSS styles applied to the page.
    
- DOM + CSSOM = Render Tree.
    

### BOM (Browser Object Model)

- Represents additional elements provided by browser (host environment) for working with everything except the document.
    
- **Examples:** `navigator`, `location`.
    
- `alert`, `confirm`, `prompt` are also part of BOM; they are not directly related to the document but are pure browser methods.
    
- BOM is part of the HTML specification.

---
## References
[^1](What%20is%20DOM,%20structure%20and%20navigation%20-%20Javascript.md)