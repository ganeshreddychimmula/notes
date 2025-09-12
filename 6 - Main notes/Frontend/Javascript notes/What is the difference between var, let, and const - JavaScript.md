
2025-07-07 15:15

Status:

Tags: [JavaScript](../../../3%20-%20Tags/JavaScript.md)

---
# What is the difference between var, let, and const - JavaScript
Here’s a **clear and simple explanation** of the differences between `var`, `let`, and `const` in JavaScript:

---

### ✅ 1. **Scope**

|Keyword|Scope|
|---|---|
|`var`|Function-scoped|
|`let`|Block-scoped (`{}`)|
|`const`|Block-scoped (`{}`)|

- **`var`** ==ignores block `{}` boundaries== — it's only scoped to the entire function or ==global==.
    
- **`let` and `const`** respect block-level scoping (like inside loops, if statements, etc.).
    

---

### ✅ 2. **Hoisting**

| Keyword | Hoisted?                        | Usable Before Declaration?                  |
| ------- | ------------------------------- | ------------------------------------------- |
| `var`   | ✅ Yes (hoisted to top of scope) | ✅ Yes (but `undefined`)                     |
| `let`   | ✅ Yes                           | ❌ No (ReferenceError in temporal dead zone) |
| `const` | ✅ Yes                           | ❌ No (ReferenceError in temporal dead zone) |

---

### ✅ 3. **Reassignment & Redeclaration**

| Keyword | Reassign? | Redeclare in Same Scope? |
| ------- | --------- | ------------------------ |
| `var`   | ✅ Yes     | ✅ Yes                    |
| `let`   | ✅ Yes     | ❌ No                     |
| `const` | ❌ No      | ❌ No                     |

- `const` must be **initialized** at declaration and cannot be **reassigned**.
    
- `let` allows reassignment but **not** redeclaration in the same scope.

- `var` allows redeclaration which might cause errors when people forgot the variable exists.

---

### 🧠 Quick Example:

```javascript
function test() {
  if (true) {
    var x = 1;
    let y = 2;
    const z = 3;
  }

  console.log(x); // ✅ 1 (function-scoped)
  console.log(y); // ❌ ReferenceError (block-scoped)
  console.log(z); // ❌ ReferenceError (block-scoped)
}
```

---

### 🔑 Summary

| Feature      | `var`           | `let`     | `const`   |
| ------------ | --------------- | --------- | --------- |
| Scope        | Function        | Block     | Block     |
| Hoisted      | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| Reassignable | Yes             | Yes       | ❌ No      |
| Redeclarable | Yes             | ❌ No      | ❌ No      |

---

### 📌 Tip

- Use **`let`** when the value will change (e.g., counters, loops).
    
- Use **`const`** by default — it communicates "this value shouldn’t be reassigned".
    
- Avoid **`var`** in modern JavaScript—it's error-prone due to its function scope and hoisting behavior.
    


---
## References