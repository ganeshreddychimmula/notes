
2025-07-15 13:17

Status:

Tags:

---
# Understand JavaScript's this Keyword in Depth - Javascript
[# Understand JavaScript's this Keyword in Depth](https://egghead.io/courses/understand-javascript-s-this-keyword-in-depth)

## this in the Global Context
- Outside of any function `this` refers to global object.
	- In browser, that is global object `window`.
- doesn't matter if we use strict or not, a top level this always refers to global object.
- In node, toplevel code of a NODE MODULE THIS IS equivalent to ` module.exports`
	- console.log(node === module.exports) => true

### this in function calls
![Pasted image 20250715133856](../Media%20and%20other%20files/Pasted%20image%2020250715133856.png)

Result: (without strict mode)
undefined
Jane // global.firstName
Doe //global.lastName

Result: (use Strict)
![Pasted image 20250715134635](../Media%20and%20other%20files/Pasted%20image%2020250715134635.png)
- Helps in avoiding accidental creation of global variables






---
## References