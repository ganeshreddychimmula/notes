
2025-07-07 18:16

Status:

Tags:

---
# null vs undefined - Javascript

## ⚖️ **`null` vs `undefined` in JavaScript**

|Feature|`null`|`undefined`|
|---|---|---|
|**Type**|Object 🧟‍♂️ (weird legacy quirk)|Undefined|
|**Meaning**|_Intentional_ absence of value|_Unintentional_ absence (not assigned)|
|**Who sets it?**|You (the developer)|JavaScript (automatically)|
|**Common Use**|Manual reset, database `null`|Uninitialized variables, missing props|
|**Boolean**|Falsy|Falsy|

---

### 🧠 In Simple Words:

- **`undefined`** means:
    
    > “JavaScript doesn't know what this is yet.”
    
- **`null`** means:
    
    > “This is **deliberately empty** or cleared out.”
    

---

### 🔍 Examples:

```js
let a;
console.log(a); // undefined (not assigned)

let b = null;
console.log(b); // null (explicitly empty)

function doSomething(x) {
  console.log(x);
}
doSomething(); // undefined (no argument passed)

let obj = {};
console.log(obj.name); // undefined (no such property)

obj.name = null;
console.log(obj.name); // null (property exists, but set to null)
```

---

### ⚠️ Equality Comparison

```js
null == undefined      // ✅ true (loose equality — considered similar)
null === undefined     // ❌ false (strict — different types)
```

---

### 📌 Real-World Example

```js
let user = {
  name: null,          // user intentionally left name empty
  age: undefined       // age was never provided or set
};
```

- `null`: The app or user explicitly cleared or left out the name.
    
- `undefined`: It was never set at all — maybe a missing input or failed fetch.
    

---

### 🔑 Key Takeaways

- Use `null` when you want to **intentionally clear or reset** a value.
    
- `undefined` shows up when a **value hasn't been assigned yet**.
    
- Both are **falsy**, but serve **different purposes** semantically.
    
- Prefer **explicit use of `null`** when you want to indicate "nothing".
    
---
## References