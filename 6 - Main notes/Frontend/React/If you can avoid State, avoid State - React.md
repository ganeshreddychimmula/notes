
2025-07-06 23:09

Status:

Tags: [React](../../../3%20-%20Tags/React.md)

---
### ✅ **“If you can avoid state, avoid state” — Meaning**

This means:

> Don’t introduce `useState`, `useReducer`, or any kind of stateful logic unless **you absolutely need to remember data between renders**.

Why?

Because **state introduces complexity**:  
- Every state update causes a **re-render**.
- You need to handle **initial values**, **state transitions**, and **effects**.
- More state = more chances for **bugs, stale data, and unnecessary re-renders**.

---

### 🎯 When NOT to use state
You **don’t need state** if:
1. The data **doesn’t change** (static content).
2. You can **compute it on the fly** from props or other values.
3. The data is **not needed across renders** (e.g., a temporary variable inside a function).

#### ❌ Example: Unnecessary state
```jsx
const [sum, setSum] = useState(a + b); // Unnecessary
```

Instead:
```jsx
const sum = a + b; // ✅ Compute from props/state
```

---

### 🧠 When to use state
Use state when:
- You need to **remember user input** (`input`, `checkbox`, etc.).
- You need to **toggle views** (e.g. `isModalOpen`).
- You fetch data and want to **store it across renders**.
- You manage UI state that **changes over time**.

---

### 📌 In short:
> Use state **only when React needs to remember something between renders.**  
> If you can derive the data instead — do it. It keeps your components clean and declarative.


---
### Live Example

### 💡 What you did:

Instead of doing this:

```jsx
const [wrongGuessCount, setWrongGuessCount] = useState(0)

// Then updating it manually:
if (wrongGuess) setWrongGuessCount(prev => prev + 1)
```

You **derived** it like this:

```jsx
const wrongGuessCount = 
  guessedLetters.filter(letter => !currentWord.includes(letter)).length
```

---

## 🧠 Why this is a smart move

### ✅ 1. **Keeps State Minimal**

Every `useState` creates more:

- Memory overhead (React must track changes)
    
- Risk of bugs (e.g. stale updates)
    
- Need for syncing: e.g., what if `guessedLetters` changes but `wrongGuessCount` didn’t?
    

But by **deriving it**, React will **always calculate it correctly from current values** — no need to remember or reset anything.

---

### ✅ 2. **Avoids Bugs**

Imagine:

```js
setGuessedLetters(["r", "e", "x"]);
setWrongGuessCount(1); // But maybe it should have been 2
```

Now `wrongGuessCount` is stale or out of sync.  
With a **derived value**, this can’t happen — it’s recalculated on every render.

---

### ✅ 3. **Improves Readability and Debuggability**

Your version is:

- **Predictable**: Always correct if `guessedLetters` and `currentWord` are accurate.
    
- **Declarative**: Reads like “what is,” not “how to update it.”
    

---

## 🚀 TL;DR: In your example:

|Aspect|Imperative state (`useState`)|Derived value (your approach)|
|---|---|---|
|Accuracy|Prone to desync|Always in sync|
|Performance|Slightly more overhead|More efficient|
|Simplicity|More moving parts|Clean, declarative|
|React’s Recommendation|Avoid unless you must|✔ Best practice|

---

### ✅ Final Verdict:

> ✔ Your approach is **correct, efficient, and idiomatic React**.

### 🔁 When should you use state instead?

Use `useState` **only when you need to store and persist values that React wouldn't otherwise re-compute or track**, like:

- form input values (unless fully controlled)
    
- toggled UI states (`isOpen`)
    
- async data after a fetch (`setData(res)`)
    

Would you like a visual cheat sheet showing when to **derive vs store** values in state?

Example used here is for this problem:
![Pasted image 20250706231606](../../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250706231606.png) 



---
## References