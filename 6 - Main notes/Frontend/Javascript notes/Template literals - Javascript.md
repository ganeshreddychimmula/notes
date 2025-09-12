
2025-07-07 19:19

Status:

Tags: [JavaScript](3%20-%20Tags/JavaScript.md)

---
# Template literals - Javascript

**Template literals** (also called **template strings**) are one of JavaScript's most useful modern features introduced in **ES6** — they make working with strings much easier and more readable.

---

## 🧠 What Are Template Literals?

> **Template literals** are string literals that allow **embedded expressions**, **multi-line strings**, and **string interpolation** using **backticks** (` ``) instead of regular quotes (`'` or `"`).

---

### ✅ Basic Syntax:

```js
const name = "Alice";
const message = `Hello, ${name}!`;
console.log(message); // "Hello, Alice!"
```

- ✅ Use backticks `` `...` ``
    
- ✅ Insert variables or expressions using `${...}`
    

---

## ✨ How Do They Help?

| Feature                        | Description & Example                                         |
| ------------------------------ | ------------------------------------------------------------- |
| ✅ **String Interpolation**     | `${...}` for easy variable or expression insertion            |
| ✅ **Multi-line Strings**       | No need for `\n` or `+` to break lines                        |
| ✅ **Readable String Building** | Cleaner and more maintainable code                            |
| ✅ **Supports Expressions**     | You can do math, function calls, ternaries, etc. inside `${}` |

---

### 🧪 Examples:

#### 1. **Simple Interpolation**

```js
const user = "Prashanth";
const greeting = `Hi, ${user}!`;
```

#### 2. **Expression Evaluation**

```js
const a = 5, b = 10;
console.log(`Sum is ${a + b}`); // Sum is 15
```

#### 3. **Function Call Inside Template**

```js
function getTime() {
  return new Date().toLocaleTimeString();
}
const msg = `Current time: ${getTime()}`;
```

#### 4. **Multi-line String**

```js
const poem = `
Roses are red,
Violets are blue,
JS with backticks,
Is easier for you.
`;
console.log(poem);
```

#### 5. **Tagged Template Literals** (Advanced)
 
```js
function tag(strings, value) {
  return `${strings[0]}--${value.toUpperCase()}--${strings[1]}`;
}
const result = tag`Hello, ${"world"}!`;
console.log(result);// Hello, --WORLD--!
```

---

### 🔥 Without Template Literals (Old Way)

```js
const name = "Alice";
const greeting = "Hello, " + name + "!"; // ❌ clunky
const multiline = "Line 1\n" + "Line 2";  // ❌ messy
```

---

## 🧠 Summary

|Feature|Old Way|Template Literals|
|---|---|---|
|String interpolation|`"Hello " + name`|`` `Hello ${name}` ``|
|Multi-line strings|`"line1\nline2"`|`` `line1\nline2` ``|
|Clean formatting|❌ Hard to manage|✅ Super readable|


---
## References