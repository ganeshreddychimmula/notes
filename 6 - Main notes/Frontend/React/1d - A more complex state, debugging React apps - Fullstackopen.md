
2025-07-15 21:13

Status:

Tags:

---
# 1d - A more complex state, debugging React apps - Fullstackopen

We can define the new state object a bit more neatly by using the [object spread](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) syntax that was added to the language specification in the summer of 2018:

```js
const handleLeftClick = () => {
  const newClicks = { 
    ...clicks, 
    left: clicks.left + 1 
  }
  setClicks(newClicks)
}

const handleRightClick = () => {
  const newClicks = { 
    ...clicks, 
    right: clicks.right + 1 
  }
  setClicks(newClicks)
}
```
Assigning the object to a variable in the event handlers is not necessary and we can simplify the functions to the following form:

```js
const handleLeftClick = () =>
  setClicks({ ...clicks, left: clicks.left + 1 })

const handleRightClick = () =>
  setClicks({ ...clicks, right: clicks.right + 1 })
```

Some  might be wondering why we didn't just update the state directly, like this:

```js
const handleLeftClick = () => {
  clicks.left++
  setClicks(clicks)
}
```

The application appears to work. However, ==it is forbidden in React to mutate state directly== since [it can result in unexpected side effects](https://stackoverflow.com/a/40309023). Changing state has to always be done by setting the state to a new object. If properties from the previous state object are not changed, they need to simply be copied, which is done by copying those properties into a new object and setting that as the new state. [^1] [^2]

### Handling arrays [^3]
**Array.concat()** - 
```js
const handleLeftClick = () => {
  setAll(allClicks.concat('L'))
  setLeft(left + 1)
}
```

The piece of state stored in _allClicks_ is now set to be an array that contains all of the items of the previous state array plus the letter _L_. Adding the new item to the array is accomplished with the [concat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) method, ==which does not mutate the existing array but rather returns a _new copy of the array_ with the item added to it.==
**Array.join(seperator)**
```js
const App = () => {
  // ...

  return (
    <div>
      {left}
      <button onClick={handleLeftClick}>left</button>
      <button onClick={handleRightClick}>right</button>
      {right}
      <p>{allClicks.join(' ')}</p>    </div>
  )
}
```

We call the [join](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join) method on the _allClicks_ array, that joins all the items into a single string, separated by the string passed as the function parameter, which in our case is an empty space.

### Update of the state is asynchronous
The reason for this is that a state update in React happens [asynchronously](https://react.dev/learn/queueing-a-series-of-state-updates), i.e. not immediately but "at some point" before the component is rendered again. [^4]
- Setting state does not change the variable in the existing render, but it requests a new render.
- React processes state updates after event handlers have finished running. This is called batching.
- To update some state multiple times in one event, you can use `setNumber(n => n + 1)` updater function.

You might expect that button will increment the counter three times because it calls `setNumber(number + 1)` three times:

```
setNumber(0 + 1);setNumber(0 + 1);setNumber(0 + 1);
```

But there is one other factor at play here. **React waits until _all_ code in the event handlers has run before processing your state updates.** This is why the re-render only happens _after_ all these `setNumber()` calls.

It is an uncommon use case, but if you would like to update the same state variable multiple times before the next render, instead of passing the _next state value_ like `setNumber(number + 1)`, you can pass a _function_ that calculates the next state based on the previous one in the queue, like `setNumber(n => n + 1)`. It is a way to tell React to “do something with the state value” instead of just replacing it.
```jsx
  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        setNumber(n => n + 1);
        setNumber(n => n + 1);
        setNumber(n => n + 1);
      }}>+3</button>
    </>
  )
```
Here, `n => n + 1` is called an **updater function.** When you pass it to a state setter:

1. React queues this function to be processed after all the other code in the event handler has run.
2. During the next render, React goes through the queue and gives you the final updated state.

Here’s how React works through these lines of code while executing the event handler:

1. `setNumber(n => n + 1)`: `n => n + 1` is a function. React adds it to a queue.
2. `setNumber(n => n + 1)`: `n => n + 1` is a function. React adds it to a queue.
3. `setNumber(n => n + 1)`: `n => n + 1` is a function. React adds it to a queue.

When you call `useState` during the next render, React goes through the queue. The previous `number` state was `0`, so that’s what React passes to the first updater function as the `n` argument. Then React takes the return value of your previous updater function and passes it to the next updater as `n`, and so on:

|queued update|`n`|returns|
|---|---|---|
|`n => n + 1`|`0`|`0 + 1 = 1`|
|`n => n + 1`|`1`|`1 + 1 = 2`|
|`n => n + 1`|`2`|`2 + 1 = 3`|

React stores `3` as the final result and returns it from `useState`.

What about this event handler? What do you think `number` will be in the next render?

```
<button onClick={() => {  setNumber(number + 5);  setNumber(n => n + 1);}}>
```
Here’s what this event handler tells React to do:

1. `setNumber(number + 5)`: `number` is `0`, so `setNumber(0 + 5)`. React adds _“replace with `5`”_ to its queue.
2. `setNumber(n => n + 1)`: `n => n + 1` is an updater function. React adds _that function_ to its queue.

During the next render, React goes through the state queue:

|queued update|`n`|returns|
|---|---|---|
|”replace with `5`”|`0` (unused)|`5`|
|`n => n + 1`|`5`|`5 + 1 = 6`|

React stores `6` as the final result and returns it from `useState`.

### Old React
In this course, we use the [state hook](https://react.dev/learn/state-a-components-memory) to add state to our React components, which is part of the newer versions of React and is available from version [16.8.0](https://www.npmjs.com/package/react/v/16.8.0) onwards. Before the addition of hooks, there was no way to add state to functional components. Components that required state had to be defined as [class](https://react.dev/reference/react/Component) components, using the JavaScript class syntax.

### Debugging React applications

Logging output to the console is by no means the only way of debugging our applications. You can pause the execution of your application code in the Chrome developer console's _debugger_, by writing the command [debugger](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/debugger) anywhere in your code.

The execution will pause once it arrives at a point where the _debugger_ command gets executed:

![debugger paused in dev tools](https://fullstackopen.com/static/4a4bced189180676ff4019f459be833e/5a190/7a.png)

By going to the _Console_ tab, it is easy to inspect the current state of variables:

![console inspection screenshot](https://fullstackopen.com/static/5ba1388f4d17134dcfc62fbeb2251421/5a190/8a.png)

Once the cause of the bug is discovered you can remove the _debugger_ command and refresh the page.

The debugger also enables us to execute our code line by line with the controls found on the right-hand side of the _Sources_ tab.

You can also access the debugger without the _debugger_ command by adding breakpoints in the _Sources_ tab. Inspecting the values of the component's variables can be done in the _Scope_-section:
![breakpoint example in devtools](https://fullstackopen.com/static/c8c143bb940ecd99aea4dc4a1c0239f2/5a190/9a.png)

### Rules of Hooks [^5]
The _useState_ function (as well as the _useEffect_ function introduced later on in the course) _must not be called_ from inside of a loop, a conditional expression, or any place that is not a function defining a component. This must be done to ensure that the hooks are always called in the same order, and if this isn't the case the application will behave erratically.

### Do Not Define Components Within Components
```js
// This is the right place to define a component
const Button = (props) => (
  <button onClick={props.onClick}>
    {props.text}
  </button>
)

const App = () => {
  const [value, setValue] = useState(10)

  const setToValue = newValue => {
    console.log('value now', newValue)
    setValue(newValue)
  }

  // Do not define components inside another component
  const Display = props => <div>{props.value}</div>
  return (
    <div>
      <Display value={value} />      <Button onClick={() => setToValue(1000)} text="thousand" />
      <Button onClick={() => setToValue(0)} text="reset" />
      <Button onClick={() => setToValue(value + 1)} text="increment" />
    </div>
  )
}
```

The application still appears to work, but **don't implement components like this!** Never define components inside of other components. The method provides no benefits and leads to many unpleasant problems. The biggest problems are because React treats a component defined inside of another component as a new component in every render. This makes it impossible for React to optimize the component.

### Web programmers oath

Programming is hard, that is why I will use all the possible means to make it easier

- I will have my browser developer console open all the time
- I progress with small steps
- I will write lots of _console.log_ statements to make sure I understand how the code behaves and to help pinpointing problems
- If my code does not work, I will not write more code. Instead I will start deleting the code until it works or just return to a state when everything was still working
- When I ask for help in the course Discord channel or elsewhere I formulate my questions properly, see [here](http://fullstackopen.com/en/part0/general_info#how-to-get-help-in-discord) how to ask for help

### Utilization of Large language models
The degree of usefulness of the hints provided by Copilot and other language models varies. Perhaps the biggest problem with language models is [hallucination](https://en.wikipedia.org/wiki/Hallucination_\(artificial_intelligence\)), they sometimes generate completely convincing-looking answers, which, however, are completely wrong. When programming, of course, the hallucinated code is often caught quickly if the code does not work. More problematic situations are those where the code generated by the language model seems to work, but it contains more difficult to detect bugs or e.g. security vulnerabilities.

Another problem in applying language models to software development is that it is difficult for language models to "understand" larger projects, and e.g. to generate functionality that would require changes to several files. Language models are also currently unable to generalize code, i.e. if the code has, for example, existing functions or components that the language model could use with minor changes for the requested functionality, the language model will not bend to this. The result of this can be that the code base deteriorates, as the language models generate a lot of repetition in the code, see more e.g. [here](https://visualstudiomagazine.com/articles/2024/01/25/copilot-research.aspx).

When using language models, the responsibility always stays with the programmer.

The rapid development of language models puts the student of programming in a challenging position: is it worth and is it even necessary to learn programming in a detailed level, when you can get almost everything ready-made from language models?

At this point, it is worth remembering the old wisdom of [Brian Kerningham](https://en.wikipedia.org/wiki/Brian_Kernighan), co-author of _The C Programming Language_:

![Everyone knows that debugging is twice as hard as writing a program in the first place. So if you're as clever as you can be when you write it, how will you ever debug it? ― Brian Kernighan](https://fullstackopen.com/static/e6925d394dfcafd08329c96230a68841/5a190/kerningham.png)





---
## References
[^1]: [Why can't I directly modify a component's state - React](6%20-%20Main%20notes/Frontend/React/Why%20can't%20I%20directly%20modify%20a%20component's%20state%20-%20React.md)
[^2]: [Choosing state structure - React](6%20-%20Main%20notes/Frontend/React/Choosing%20state%20structure%20-%20React.md)
[^3]: [How React handles or renders Arrays](6%20-%20Main%20notes/Frontend/React/How%20React%20handles%20or%20renders%20Arrays.md)
[^4]: [Queueing a Series of State Updates - React](6%20-%20Main%20notes/Frontend/React/Queueing%20a%20Series%20of%20State%20Updates%20-%20React.md)
[^5]: [Why shouldn't we use hooks inside loops or conditions - React](6%20-%20Main%20notes/Frontend/React/Why%20shouldn't%20we%20use%20hooks%20inside%20loops%20or%20conditions%20-%20React.md)