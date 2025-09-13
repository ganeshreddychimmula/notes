
2025-06-24 11:27

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

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
[Why do we need to different files (index.jsx and app.jsx) in React projects](../../../6%20-%20Main%20notes/Frontend/React/Why%20do%20we%20need%20to%20different%20files%20(index.jsx%20and%20app.jsx)%20in%20React%20projects.md)
[CreateElement React](../../../6%20-%20Main%20notes/Frontend/React/CreateElement%20React.md)
[2 - JSX React](../../../6%20-%20Main%20notes/Frontend/React/2%20-%20JSX%20React.md)
[Why mostly React](../../../6%20-%20Main%20notes/Frontend/React/Why%20mostly%20React.md)		
[Creating a React Component](../../../6%20-%20Main%20notes/Frontend/React/Creating%20a%20React%20Component.md)