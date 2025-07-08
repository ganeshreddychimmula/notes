
2025-07-08 18:56

Status:

Tags: [[JavaScript]]

---
# DOM - Javascript
### DOM (Document Object Model) 

- The Document Object Model represents all page content as objects that can be modified.
- `document` → main entry point to the page.
    - Can create or change anything on the page.
- The DOM specification explains the **structure of a document** and provides objects to manipulate it.
- There are non-browser environments that use DOM too.

### DOM Tree Structure

- Every HTML tag is an object.
	- Nested tags are children of the enclosing one
	- A tag inside a tag is also an object.
- Spaces and newlines are valid characters, like letters and digits.
    - They form text nodes and become part of the DOM.
    - Spaces and newlines before `<head>` are ignored.    
    - If content is placed after `<body>`, it is automatically moved inside the `<body>`.
- Browser tools that work with DOM usually do not show spaces at the start/end of text and empty text nodes (line-breaks) between tags.
- If the browser encounters malformed HTML, it automatically corrects it when creating the DOM.
    - For example, the top tag is always `<html>`, even if not specified.
    - While generating DOM, browsers automatically process errors in the document, like closing tags.
        
### Core DOM Nodes

- Browser automatically creates `<body>` in `<table>` if missing.
- Everything in HTML becomes part of the DOM.
- ==The `document` object is also part of the DOM tree.==
- There are 12 node types. In practice, we usually work with 4 of them:
    1. `document`: The entry point of HTML.
    2. `element nodes`: HTML tags, the tree building blocks.
    3. `text nodes`.
    4. `comments`.
- To select an element in the browser console: `ESC` (opens console) → `$0` (current selected element).
    
### DOM Hierarchy and Navigation
![[PXL_20250708_234146994.jpg]]
                
- The topmost tree nodes are available as document properties:
    - `<html>` = `document.documentElement`
    - `<body>` = `document.body`
    - `<head>` = `document.head`
        
- `document.body` can be `null` when scripts are inside `<head>` and the browser hasn't fully read the HTML yet.
    
### Node Navigation Properties

- `childNodes`: All elements that are direct children, including text nodes.
- `descendants`: All elements that are nested in the given one, including children, their children, and so on.
- **Properties:** `firstChild`, `lastChild`
    - `elem.childNodes[0]` → `elem.firstChild`
    - `elem.childNodes[elem.childNodes.length - 1]` → `elem.lastChild`
- `elem.hasChildNodes()`: Checks whether any child node exists.
- `elem.childNodes`: Not an array, but an array-like iterable collection. Array methods won't work directly on it.
- DOM collections[^1] are read-only. -> **All navigation properties are read-only.**
- DOM collections are live (reflect real-time changes).
- Avoid `for...in` loops on DOM collections as it goes over all enumerable properties, and they may have extra non-node properties.

### Element-Only Navigation

- `nextSibling` → right sibling (can be text node, comment, etc.)
- `previousSibling` → left sibling (can be text node, comment, etc.)
- `parentNode` → parent of the node (can be `document` for `<html>`)
    
- **Navigation of only Elements:**
    - `elem.children`: Only those children that are element nodes.
    - `firstElementChild`, `lastElementChild`: First and last child _element_.
    - `previousElementSibling`
    - `nextElementSibling`
    - `parentElement`

### `parentNode` vs `parentElement`

- All same except one case:
    - `document.documentElement.parentNode` // `document`
    - `document.documentElement.parentElement` // `null`
- This is because `document` is not an element node.
- `document` -> entry point to the page.
- `document.documentElement` -> root element of html document -> `<html>`
	- A DOM property that gives direct access to `<html>` element.
	- Top-most element (not the top most node) in DOM tree.

### Table-Specific Properties

- `table.rows` → collection of `<tr>` elements.
- `table.caption` / `tHead` / `tFoot` → `<caption>`, `<thead>`, `<tfoot>` elements.
- `table.tBodies` → collection of `<tbody>` elements.
    - Will be created even if not specified in the HTML document.
- `<thead>`, `<tfoot>`, `<tbody>` elements provide the `rows` property.
- `tr.cells` → collection of `<td>` & `<th>` cells.
- `tr.sectionRowIndex` → position of the given `tr` inside its enclosing (`<thead>`, `<tbody>`, `<tfoot>`).
- `tr.rowIndex`
    
### Searching the DOM

- `document.getElementById(id)`
- `elem.querySelectorAll(query)`: Returns all elements inside `elem` matching the CSS selector.
    - Pseudo-classes in CSS like `:hover` and `:active` are supported.
- `elem.querySelector(query)`: Returns the first element inside `elem` matching the given CSS selector.
- `elem.matches(css_selector)`: Returns `true` or `false`.
    - Merely checks if `elem` matches the given CSS selector.
- `elem.closest(css_selector)`: Returns the closest ancestor that matches the CSS selector.
    - `elem` itself is also part of the search.
- `elemA.contains(elemB)`: Checks if `elemA` contains `elemB`.

---
## References
[^1]: [[DOM Collection - Javascript]]
