
2025-06-24 22:34

Status:

Tags:

---
# JSX elements must have a single common parent when being returned from a component or rendered directly.
![Pasted image 20250624223432](../../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250624223432.png)

In JSX, only **one top-level element** is allowed per return statement because JSX compiles down to `React.createElement()`, which must return a single root node.

---
## References
[Fragment - A workaround for common parent Requirement](Fragment%20-%20A%20workaround%20for%20common%20parent%20Requirement.md)