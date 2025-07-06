
2025-07-05 23:44

Status #ReadLater 

Tags:

---
# You might not need an Effect - React

[^1]: [React Docs - You might not need an  effect](https://react.dev/learn/you-might-not-need-an-effect) 
- It isn't suggested to use effect when there is no external synchronization involved.
- Effects are an escape hatch from the React paradigm. They let you “step outside” of React and synchronize your components with some external system like a non-React widget, network, or the browser DOM. If there is no external system involved (for example, if you want to update a component’s state when some props or state change), you shouldn’t need an Effect. Removing unnecessary Effects will make your code easier to follow, faster to run, and less error-prone.[^1]

---
## References