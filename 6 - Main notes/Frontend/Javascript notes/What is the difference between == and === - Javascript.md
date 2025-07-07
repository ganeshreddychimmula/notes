
2025-07-07 18:07

Status:

Tags: [[JavaScript]]

---
# What is the difference between == and === - Javascript

## ✅ `==` vs `===` in JavaScript

| Operator | Name            | Compares     | Performs Type Conversion? |
| -------- | --------------- | ------------ | ------------------------- |
| `==`     | Loose Equality  | Value only   | ✅ Yes (type coercion)     |
| `===`    | Strict Equality | Value + Type | ❌ No                      |

---

### 🧠 **In Simple Words:**

- `==` says: “Are these values **equal**, even if I have to **convert their types** to match?”
    
- `===` says: “Are these values **equal in both type and value**, no conversions allowed?”
    

---

### 🔍 Examples:

```js
'5' == 5        // ✅ true  → string '5' is coerced to number 5
'5' === 5       // ❌ false → different types (string !== number)

false == 0      // ✅ true  → false is coerced to 0
false === 0     // ❌ false → different types

null == undefined  // ✅ true (special case)
null === undefined // ❌ false

0 == ''         // ✅ true  → '' coerces to 0
0 === ''        // ❌ false

[] == false     // ✅ true  → [] is coerced to '' → 0 → false
[] === false    // ❌ false
```

---

### ⚠️ Why You Should **Prefer `===`** (Strict Equality)

Using `==` can lead to **unexpected bugs**, because JavaScript silently tries to **convert types** for you, which isn't always predictable.

```js
if (value == false) {
  // May run even when value is "", 0, null, or undefined — risky!
}
```

Instead:

```js
if (value === false) {
  // Only runs if value is exactly the Boolean false
}
```

---

### 📌 Key Takeaways

- Use **`===`** unless you have a **very specific reason** to use `==`.
    
- `==` can **hide bugs** due to implicit type conversion.
    
- Understanding `==` helps you debug weird edge cases, but **write code with `===` for clarity**.
    

---
## References