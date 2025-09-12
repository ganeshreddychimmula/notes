
2025-06-30 16:58

Status:

Tags:

---
## 🎯 **Title: How React Uses State to Control the UI**
![Pasted image 20250630170134](2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250630170134.png)

---

> **Slide Opening (Big Idea):**  
> React follows a simple but powerful mental model:  
> **“Your UI is just a function of state.”**

This means — whatever your component **returns** (the view) is completely **determined by its current state**.

---

### 🔹 **Point 1: Render**

> React runs your component like a function and returns what it should display.

This render only happens again if:

- It gets **new props** from its parent  
    **OR**
- Its **state changes** inside the component.
    

So if nothing changes — React doesn’t waste time re-rendering it.

---

### 🔹 **Point 2: setState**

> Regular variables don’t trigger re-renders — only **state changes** do.

That’s why React gives you `useState()` with a `setState` function.  
Calling `setState` tells React:  
**“Hey, something changed. Please re-run the function and show the new result.”**

---

### 🔹 **Point 3: view = function(state)**

> This is the core idea:  
> When `state` changes, React re-runs your component,  
> and returns a **new version of the UI** to replace the old one.

You never manually update the DOM — you just update state, and React handles the rest.

---

### ✅ **Closing Summary (in one line):**

> **You don’t tell React how to update the DOM — you just tell it what the state is, and React figures out what to show.**

---
## References