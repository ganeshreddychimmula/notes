
2025-08-17 23:13

Status:

Tags:

---
# Compound components with dot syntax - React
Compound components with dot syntax are a **powerful design pattern** in React for creating **declarative, flexible, and intuitive APIs** for components that are tightly coupled in behavior and structure.

---
## 🧩 What are Compound Components?

**Compound components** are a group of React components that work together as a unit but are designed to be composed by the consumer of the component, rather than hardcoded internally.

### 🔧 Example

```jsx
<Tabs>
  <Tabs.Tab label="Tab 1" />
  <Tabs.Tab label="Tab 2" />
  <Tabs.Panel>Content for Tab 1</Tabs.Panel>
  <Tabs.Panel>Content for Tab 2</Tabs.Panel>
</Tabs>
```

Here, `Tabs` is the **parent** component, and `.Tab` and `.Panel` are **compound children** that participate in shared logic via **context** or other internal coordination.

---

## ✅ Why Use Compound Components with Dot Syntax?

### 1. **Declarative and Intuitive API**

- Users can structure components in a way that **mimics the UI layout**.
    
- It's **easy to read** and **self-documenting**.

### 2. **Shared Internal State**

- Parent component holds shared state (like which tab is active) and **implicitly passes it down** to children using `React.Context`.
    
- No need to pass props manually between child components.

### 3. **Encapsulation of Logic**

- Logic like tab switching, accordion toggling, or dropdown selection lives in the parent.
    
- Consumers only describe **what they want**, not how it works.

### 4. ****Better DX (Developer Experience)**

- Dot syntax makes it clear what components are part of a group.
    
- Autocompletion and intellisense support is improved in editors like VS Code.

---

## 🔄 How It Works Internally

1. **Define Context** in the parent component.
    
2. **Provide context value** from parent.
    
3. **Children consume context** via `useContext()`.
    
4. **Attach child components to the parent** as properties using dot syntax.

---

## 🔨 Example Implementation

```jsx
// Tabs.js
const TabsContext = React.createContext();

function Tabs({ children }) {
  const [activeIndex, setActiveIndex] = React.useState(0);
  return (
    <TabsContext.Provider value={{ activeIndex, setActiveIndex }}>
      <div className="tabs">{children}</div>
    </TabsContext.Provider>
  );
}

function Tab({ label, index }) {
  const { activeIndex, setActiveIndex } = React.useContext(TabsContext);
  return (
    <button
      className={index === activeIndex ? 'active' : ''}
      onClick={() => setActiveIndex(index)}
    >
      {label}
    </button>
  );
}

function Panel({ children, index }) {
  const { activeIndex } = React.useContext(TabsContext);
  return activeIndex === index ? <div>{children}</div> : null;
}

// Attach compound components
Tabs.Tab = Tab;
Tabs.Panel = Panel;

export default Tabs;
```

### Usage:

```jsx
<Tabs>
  <Tabs.Tab label="Tab A" index={0} />
  <Tabs.Tab label="Tab B" index={1} />
  <Tabs.Panel index={0}>This is Tab A</Tabs.Panel>
  <Tabs.Panel index={1}>This is Tab B</Tabs.Panel>
</Tabs>
```

---

## 🧠 Related Patterns and Concepts

- **Slot pattern**: Used for similar flexibility but often with named props or special children.
    
- **Render props**: Allows similar flexibility but with a function-based approach.[^1]
    
- **Headless UI Libraries**: (e.g., Radix, HeadlessUI) use compound components extensively. [^2]
    
- **Context API**: Core to how compound components communicate.

---

## 🔍 When to Use

Use compound components with dot syntax when:

- You have **multiple components that must share internal state**.
    
- * You want the **consumer to control composition**, but not behavior.
    
- You’re building **reusable UI libraries or design systems** (e.g., dropdowns, modals, tabs, accordions, wizards).


---
## References
[^1](Render%20props%20-%20React.md)
[^2](Headless%20Components%20-%20React.md)