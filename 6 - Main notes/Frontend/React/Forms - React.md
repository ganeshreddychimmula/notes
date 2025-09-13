
2025-07-01 12:41

Status:

Tags:[React](../../../3%20-%20Tags/React.md) [JavaScript](../../../3%20-%20Tags/JavaScript.md)

---
# Forms - React
## React Forms – Expanded Notes

### 🚫 preventDefault()
- `event.preventDefault()` prevents the default browser behavior — like reloading the page on form submit.
- It's essential in React forms where**you want to handle form submission yourself**, rather than letting the browser post the form somewhere.
 
---

### 💡 "React forms were bad, but good now"
- In older versions of React, forms were hard to manage because every input required state and event handling.
- With improvements (especially React 18+ and 19), forms have become simpler through `FormData`, `defaultValue`, and native handling in `action`.

---

## 🧱 Form Basics
```jsx
<label>Email:
  <input type="email" name="email" placeholder="joe@schmoe.com" />
</label>
```

- Labels improve accessibility and allow screen readers to link the input with the description.
- You can either:
  - Use `<label>` around the input
  - Or use `aria-label` or `htmlFor` with `id` on the input

### ⚠️ Label Differences in React
- In **HTML**:
```html
<label for="email">Email:</label>
<input name="email" />
```
- In **React**, `for` becomes `htmlFor`, and inputs must have matching `id`s:
```jsx
<label htmlFor="email">Email:</label>
<input id="email" name="email" />
```

### 🖱 Button vs Input Submit
- Both `<button>` and `<input type="submit">` work as submit buttons inside a `<form>`.

---

## 📤 Form Submission
- `method="POST"` sends data in the request body.
- `method="GET"` appends data in the URL query.
- Capitalization (POST vs post) is convention; both work.

### 📦 Manual Submission (React ≤18)
```jsx
function handleSubmit(event) {
  event.preventDefault();
  const formEl = event.currentTarget;
  const formData = new FormData(formEl);
  const email = formData.get("email");
  console.log(email);
  formEl.reset();
}
```

```jsx
<form onSubmit={handleSubmit} method="POST">...
```

---

## 🧪 React 19 – Native Form Handling
- React 19 introduces support for `action={function}` for forms.
- No need for `onSubmit` or `preventDefault()` manually.

### ✅ React 19 Example:
```jsx
function App() {
  function signUp(formData) {
    const email = formData.get("email");
	    // automatic: preventDefault(), reset(), formData creation
  }

  return (
    <form action={signUp}>
      <input name="email" type="email" />
      <button>Submit</button>
    </form>
  );
}
```

**React handles:**
1. `event.preventDefault()`
2. `const formData = new FormData(form)`
3. `form.reset()`

---

## 🧓 React ≤18 Manual Form Handling
- Requires `onSubmit={handleSubmit}`
- Must manually call `preventDefault()` and build `FormData`
- Every field must be tracked individually if you need dynamic state updates

---

## 📄 Tracking Inputs (Old Method)
```jsx
const [email, setEmail] = useState('');
<input value={email} onChange={e => setEmail(e.target.value)} />
```
- Every input needs:
  - A state variable
  - An `onChange` handler
  - A `value` prop

---

## 📝 TextArea and Default Values
```jsx
<label htmlFor="description">Description:</label>
<textarea id="description" name="description"></textarea>
```
- Textareas are used for multi-line input.
- Use `defaultValue="Text here"` to prepopulate the field.

---

## 🔘 Radio Buttons
```jsx
<fieldset>
  <legend>Employment Status</legend>

  <label>
    <input type="radio" name="employmentStatus" value="unemployed" />
    Unemployed
  </label>

  <label>
    <input type="radio" name="employmentStatus" value="part-time" />
    Part-time
  </label>

  <label>
    <input type="radio" name="employmentStatus" value="full-time" defaultChecked />
    Full-time
  </label>
</fieldset>
```

- `name` groups radios
- `value` determines the data stored in `formData`
- `defaultChecked` sets the default selected radio

---

## ☑️ Checkboxes
```jsx
<fieldset>
  <legend>Dietary Restrictions</legend>
  <label>
    <input type="checkbox" name="dietaryRestrictions" value="kosher" /> Kosher
  </label>
  <label>
    <input type="checkbox" name="dietaryRestrictions" value="vegan" /> Vegan
  </label>
  <label>
    <input type="checkbox" name="dietaryRestrictions" value="gluten-free" defaultChecked /> Gluten-Free
  </label>
</fieldset>
```

```jsx
const dietaryRestrictions = formData.getAll("dietaryRestrictions");
```
- ✅ Use `formData.getAll()` to get **multiple selected values**
- `formData.get("...")` would return only one 
- [^1]

---

## 🔽 Select Dropdown
```jsx
<label htmlFor="favColor">Favorite Color:</label>
<select id="favColor" name="favColor" defaultValue="">
  <option value="" disabled>-- Choose a color --</option>
  <option value="red">Red</option>
  <option value="orange">Orange</option>
  <option value="yellow">Yellow</option>
  <option value="green">Green</option>
  <option value="blue">Blue</option>
  <option value="indigo">Indigo</option>
  <option value="violet">Violet</option>
</select>
```

```js
const favColor = formData.get("favColor")
```
- Use `defaultValue` to set a default selection
- `disabled` + `value=""` prevents choosing the placeholder option

---





---
## References

[^1]: [object.fromEntries() - javaScript](../Javascript%20notes/object.fromEntries()%20-%20javaScript.md)
