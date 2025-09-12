
2025-07-02 19:23

Status:

Tags:

---
# Controlled Components - React

## 🎛️ Controlled Components in React – Explained with Examples

### 🧠 What Are Controlled Components?

In React, **controlled components** are form[^1] inputs (`<input>`, `<textarea>`, `<select>`, etc.) whose **value is controlled by React state**.

---

### ✅ Key Characteristics

- React is the **single source of truth** for the input’s value.
    
- You must use `value={state}` and `onChange={handler}` to read and update the value.
    
- This lets you respond to input changes **immediately**, **validate data**, or **trigger side effects**.
    

---

### 📦 Default vs Controlled Forms

| Feature                        | Uncontrolled (default HTML) | Controlled (React)              |
| ------------------------------ | --------------------------- | ------------------------------- |
| Input manages its own state    | ✅ Yes                       | ❌ No – React manages it         |
| Uses `value` + `onChange`      | ❌ No                        | ✅ Yes                           |
| Allows real-time updates/logic | ❌ Hard                      | ✅ Easy                          |
| Preferred for form logic       | ❌ Only for simple forms     | ✅ For validation, live previews |

---

### 🧪 Meme Generator Example Breakdown

#### 🧱 Initial State

```js
const [meme, setMeme] = useState({
  topText: "Something different",
  bottomText: "Walk into Mordor",
  imageUrl: "http://i.imgflip.com/1bij.jpg"
})
```

The `meme` object holds all form input values and the image being displayed.

---

#### ✏️ Controlled Input Example

```jsx
<input
  type="text"
  name="topText"
  placeholder="One does not simply"
  value={meme.topText}
  onChange={handleChange}
/>
```

- The input's **value** comes from React state (`meme.topText`)
    
- On typing, it **doesn’t change by itself**
    
- Instead, `onChange` triggers the handler to update the state
    

---

#### 🔁 The `handleChange` Function

```jsx
function handleChange(event) {
  const { name, value } = event.target;

  setMeme(prevMeme => ({
    ...prevMeme,
    [name]: value  // topText or bottomText dynamically updated
  }));
}
```

> This pattern allows you to handle **multiple inputs with one handler**.

---

### 👀 Why We Need Controlled Components

Without `value={meme.topText}`, the input behaves as **uncontrolled**. If the state changes for any reason (e.g. clicking a new meme image button), the UI may **not reflect it**, causing **desynchronization** between the input field and the meme display.

---

### 🧠 Benefits

- Real-time input validation
    
- Conditional logic (disable button, limit text, etc.)
    
- Easy reset (just reset the state!)
    
- Keeps UI and logic **in sync**
    

---

### 💡 Real-Life Scenarios

- Live preview of a comment or post
    
- Form validation (e.g. “password too short”)
    
- Dynamic filters/search
    
- Conditional submission logic
    

---

### ⚠️ When to Use Uncontrolled Instead

- You don’t care about every keystroke (e.g., simple form with native submit)
    
- You’re integrating with non-React libraries that manipulate DOM directly
    
- Performance is a concern (controlled components re-render on every change)
    

---

### 🧪 Bottom Line: Controlled > Uncontrolled (in React projects)

Use **controlled components** for:

- Consistency
    
- Predictability
    
- Better debugging
    
- Real-time interactions
    

---

```jsx
import { useState } from "react"

export default function Main() {

    const [meme, setMeme] = useState({

        topText: "Something different",

        bottomText: "Walk into Mordor",

        imageUrl: "http://i.imgflip.com/1bij.jpg"

    })

    function handleChange(event) {

        const {value} = event.currentTarget

        setMeme(prevMeme => ({

            ...prevMeme,

            topText: value

        }))

    }

  

    return (

        <main>

            <div className="form">

                <label>Top Text

                    <input

                        type="text"

                        placeholder="One does not simply"

                        name="topText"

                        onChange={handleChange}

                        value={meme.topText} // Using thiws mean contrololled component

                    />

                </label>

  

                <label>Bottom Text

                    <input

                        type="text"

                        placeholder="Walk into Mordor"

                        name="bottomText"

                    />

                </label>

                <button>Get a new meme image 🖼</button>

            </div>

            <div className="meme">

                <img src={meme.imageUrl} />

                <span className="top">{meme.topText}</span>

                <span className="bottom">{meme.bottomText}</span>

            </div>

        </main>

    )

}

```
![Pasted image 20250702191627](2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250702191627.png)


---
## References

[^1]: [Forms - React](6%20-%20Main%20notes/Frontend/React/Forms%20-%20React.md)