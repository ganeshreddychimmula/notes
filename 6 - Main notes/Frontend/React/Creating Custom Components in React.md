
2025-06-25 13:23

Status:

Tags:

---
# Creating Custom Components in React
- Creating multiple single purpose components is great for composability and reusability.
- For custom components in React we need to use a pascal case, which is similar to camel case, where you remove spaces for multi word names and make the space stripped words first letter capital, in addition to that in pascal case we also make 
	- eg: `move to right -> camelCase - moveToRight -> PascalCase - MoveToRight`
- While these components are declared as functions that return JSX, we need to call them as  HTML elements with `< />`(angel brackets). You cannot call them as regular JavaScript functions.
- Calling React components as enclosed HTML elements (e.g., `<Page />` or `<Page></Page>`) is a [React convention](https://scrimba.com/learn-react-c0e/~03vw) that leverages JSX syntax. While JSX allows for HTML-like syntax, the specific practice of using custom, capitalized tags for components is how React differentiates them from standard HTML elements and enables their rendering.
	- eg:![Pasted image 20250625133814](2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250625133814.png)

---
## References
[Composability in React and why its important](6%20-%20Main%20notes/Frontend/React/Composability%20in%20React%20and%20why%20its%20important.md)