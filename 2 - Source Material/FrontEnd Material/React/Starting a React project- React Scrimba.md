
2025-06-24 11:27

Status:

Tags: [[React]]

---
# Setting up index page
- Instead of adding anything to our markup manually,  react will be in charge of taking our JavaScript and adding the associated markup to our HTML document for us.
- Setup React in Index.JSX file
	1. Create a root
	2. Render some markup to the root.
```js
import { createRoot } from "react-dom/client"

const root = createRoot(document.getElementById("root"))

root.render(<h1>Hello, React!</h1>)
```
- `const root = createRoot(document.getElementById("root"))` Where to eventually render the markup
- `root.render()` - tells what to render




---
## References
[[Why do we need to different files (index.jsx and app.jsx) in React projects]]
[[CreateElement React]]
[[(2) JSX React]]
[[Why mostly React]]		
[[Creating a React Component]]