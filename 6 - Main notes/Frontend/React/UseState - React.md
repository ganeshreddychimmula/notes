
2025-07-01 11:11

Status:

Tags: [Hooks](Hooks) [React](../../../3%20-%20Tags/React.md)]

---
# UseState - React
[UseState React official doc](https://react.dev/reference/react/useState)

- Inorder to declare state variable you need `useState`.
- Call `useState` at the top level of your component to declare a [state variable.](https://react.dev/learn/state-a-components-memory)

```jsx
import { useState } from 'react';

function MyComponent() {  
const [age, setAge] = useState(28);  
const [name, setName] = useState('Taylor');  
const [todos, setTodos] = useState(() => createTodos());  // ...
```

The convention is to name state variables like `[something, setSomething]` using [array destructuring.](https://javascript.info/destructuring-assignment)

[](https://react.dev/reference/react/useState#usage)

#### Parameters [](https://react.dev/reference/react/useState#parameters%20"Link%20for%20Parameters")

- `initialState`: The value you want the state to be initially. It can be a value of any type, but there is a special behavior for functions. This argument is ignored after the initial render.
    - If you pass a function as `initialState`, it will be treated as an _initializer function_. It should be pure, should take no arguments, and should return a value of any type. React will call your initializer function when initializing the component, and store its return value as the initial state. [](https://react.dev/reference/react/useState#avoiding-recreating-the-initial-state)  [^1]

#### Returns [](https://react.dev/reference/react/useState#returns%20"Link%20for%20Returns")

`useState` returns an array with exactly two values:

1. The current state. During the first render, it will match the `initialState` you have passed.
2. The [](https://react.dev/reference/react/useState#setstate) that lets you update the state to a different value and trigger a re-render.

#### Caveats [](https://react.dev/reference/react/useState#caveats%20"Link%20for%20Caveats")

- `useState` is a Hook, so you can only call it **at the top level of your component** or your own Hooks. You can’t call it inside loops or conditions. If you need that, extract a new component and move the state into it. [^1]
- In Strict Mode, React will **call your initializer function twice** in order to [](https://react.dev/reference/react/useState#my-initializer-or-updater-function-runs-twice) This is development-only behavior and does not affect production. If your initializer function is pure (as it should be), this should not affect the behavior. The result from one of the calls will be ignored.

### `set` functions, like `setSomething(nextState)` [](https://react.dev/reference/react/useState#setstate%20"Link%20for%20this%20heading")

The `set` function returned by `useState` lets you update the state to a different value and trigger a re-render. You can pass the next state directly, or a function that calculates it from the previous state:

```jsx
const [name, setName] = useState('Edward');
function handleClick() {  
	setName('Taylor');  
	setAge(a => a + 1);
	}  // ...
```

#### Parameters [](https://react.dev/reference/react/useState#setstate-parameters%20"Link%20for%20Parameters")

- `nextState`: The value that you want the state to be. It can be a value of any type, but there is a special behavior for functions.
    - If you pass a function as `nextState`, it will be treated as an _updater function_. It must be pure, should take the pending state as its only argument, and should return the next state. React will put your updater function in a queue and re-render your component. During the next render, React will calculate the next state by applying all of the queued updaters to the previous state. [](https://react.dev/reference/react/useState#updating-state-based-on-the-previous-state)

#### Returns [](https://react.dev/reference/react/useState#setstate-returns%20"Link%20for%20Returns")

`set` functions do not have a return value.

#### Caveats [](https://react.dev/reference/react/useState#setstate-caveats%20"Link%20for%20Caveats")

- The `set` function **only updates the state variable for the _next_ render**. If you read the state variable after calling the `set` function, [](https://react.dev/reference/react/useState#ive-updated-the-state-but-logging-gives-me-the-old-value) that was on the screen before your call. [^2]
    
- If the new value you provide is identical to the current `state`, as determined by an [`Object.is`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is) comparison, React will **skip re-rendering the component and its children.** This is an optimization. Although in some cases React may still need to call your component before skipping the children, it shouldn’t affect your code. [^2]
    
- **React [batches state updates.](https://react.dev/learn/queueing-a-series-of-state-updates)** It updates the screen **after all the event handlers have run** and have called their `set` functions. This prevents multiple re-renders during a single event. In the rare case that you need to force React to update the screen earlier, for example to access the DOM, you can use [`flushSync`.](https://react.dev/reference/react-dom/flushSync) [^2]
    
- The `set` function has a stable identity, so you will often see it omitted from Effect dependencies, but including it will not cause the Effect to fire. If the linter lets you omit a dependency without errors, it is safe to do. [](https://react.dev/learn/removing-effect-dependencies#move-dynamic-objects-and-functions-inside-your-effect)
    
- Calling the `set` function _during rendering_ is only allowed from within the currently rendering component. React will discard its output and immediately attempt to render it again with the new state. This pattern is rarely needed, but you can use it to **store information from the previous renders**. [](https://react.dev/reference/react/useState#storing-information-from-previous-renders)
    
- In Strict Mode, React will **call your updater function twice** in order to [](https://react.dev/reference/react/useState#my-initializer-or-updater-function-runs-twice) This is development-only behavior and does not affect production. If your updater function is pure (as it should be), this should not affect the behavior. The result from one of the calls will be ignored.

---
## References
[^1](Why%20shouldn't%20we%20use%20hooks%20inside%20loops%20or%20conditions%20-%20React.md)
[^2](Batching%20in%20React%20-%20Understanding%20how%20react%20efficiently%20updates%20UI.md)
