
2025-07-07 18:19

Status:

Tags: [JavaScript](../../../3%20-%20Tags/JavaScript.md)

---
# Event delegation - JavaScript

### 🧠 **What is Event Delegation? 

> **Event Delegation** is a pattern where instead of adding event listeners to many individual child elements, you add **one event listener to a common parent** and **use `event.target` to detect which child triggered the event.**

---

### 📦 Analogy: The Waiter

Imagine you're at a restaurant where:

- Each table has **10 buttons** for ordering (starter, main, dessert...).
    
- You could assign **1 waiter per button** (bad idea 💸)
    
- Instead, you assign **one smart waiter per table** 🧠. He listens to **all clicks**, then looks at **which button was clicked**.
    

This is **event delegation**.

---

### 🧪 **Example Without Delegation (Bad)**

```js
const buttons = document.querySelectorAll('button');

buttons.forEach(btn => {
  btn.addEventListener('click', () => {
    console.log('Button clicked:', btn.textContent);
  });
});
```

- ✅ Works
    
- ❌ Not scalable if there are 100s or dynamic buttons
    

---

### ✅ **Example With Event Delegation (Better)**

```html
<ul id="menu">
  <li>Home</li>
  <li>About</li>
  <li>Contact</li>
</ul>
```

```js
document.getElementById("menu").addEventListener("click", function (e) {
  if (e.target.tagName === "LI") {
    console.log("Clicked:", e.target.textContent);
  }
});
```

- Only one event listener on `#menu`
    
- Even if new `<li>` elements are added dynamically, this still works!
    

---

### 🔄 **How It Works (Under the Hood)**

1. When an event is triggered on a child (e.g., a `<li>`),
    
2. It **bubbles up** the DOM (unless stopped),
    
3. You catch it on the parent (e.g., `<ul>`),
    
4. Then use `event.target` to find **which child was clicked**.
    

---

### 🧠 Benefits of Event Delegation

|✅ Benefit|🧠 Explanation|
|---|---|
|Performance|Fewer event listeners = faster, less memory usage|
|Works with dynamic DOM|Even elements added later will trigger the event|
|Cleaner code|Easier to manage, especially in lists or tables|

---

### ⚠️ Gotchas

- Events like `blur`, `focus`, `mouseenter`, `mouseleave` **don’t bubble**, so can't be delegated easily.
    
- Always **check `event.target`** to filter clicks to the intended child elements.
    

---

### 📌 Summary

> **Event Delegation = One parent listener + Smart filtering of events from child elements**

✅ Use it for:

- Lists (menus, comments, notifications)
    
- Tables
    
- Dynamically added buttons/fields
    

---
![ChatGPT Image Jul 7, 2025, 06_21_47 PM](../../../2%20-%20Source%20Material/Media%20and%20other%20files/ChatGPT%20Image%20Jul%207,%202025,%2006_21_47%20PM.png)


---
## References