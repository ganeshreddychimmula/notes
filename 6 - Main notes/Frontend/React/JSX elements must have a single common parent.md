
2025-06-24 22:34

Status:

Tags:

---
# JSX elements must have a single common parent when being returned from a component or rendered directly.
![[Pasted image 20250624223432.png]]

In JSX, only **one top-level element** is allowed per return statement because JSX compiles down to `React.createElement()`, which must return a single root node.

---
## References
[[Fragment - A workaround for common parent Requirement]]