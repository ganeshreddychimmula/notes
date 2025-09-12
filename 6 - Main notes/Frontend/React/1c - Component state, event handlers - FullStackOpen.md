
2025-07-15 20:08

Status:

Tags:

---
# 1c - Component state, event handlers - FullStackOpen

### Destructuring
[Destructuring Concept](../Javascript%20notes/Destructuring%20Concept.md)

### Passing state - to child components
It's recommended to write React components that are small and reusable across the application and even across projects
One best practice in React is to [lift the state up](https://react.dev/learn/sharing-state-between-components) in the component hierarchy. The documentation says:

> _Often, several components need to reflect the same changing data. We recommend lifting the shared state up to their closest common ancestor._

The event handler is passed to the _Button_ component through the _onClick_ prop. When creating your own components, you can theoretically choose the prop name freely. However, our naming choice for the event handler was not entirely arbitrary.

React's own official [tutorial](https://react.dev/learn/tutorial-tic-tac-toe) suggests: "In React, it’s conventional to use _onSomething_ names for props which take functions which handle events and handleSomething for the actual function definitions which handle those events."






---
## References