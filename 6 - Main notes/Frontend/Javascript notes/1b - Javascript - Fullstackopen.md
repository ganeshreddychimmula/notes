
2025-07-14 20:52

Status:

Tags: [JavaScript](../../../3%20-%20Tags/JavaScript.md)

---
# 1b - Javascript - Fullstackopen
- The official name of the JavaScript standard is [ECMAScript](https://en.wikipedia.org/wiki/ECMAScript). At this moment, the latest version is the one released in June of 2024 with the name [ECMAScript®2024](https://www.ecma-international.org/ecma-262/), otherwise known as ES15.
- Browsers do not yet support all of JavaScript's newest features. Due to this fact, a lot of code run in browsers has been _transpiled_ from a newer version of JavaScript to an older, more compatible version.
- Today, the most popular way to do transpiling is by using [Babel](https://babeljs.io/). Transpilation is automatically configured in React applications created with Vite.
- [Node.js](https://nodejs.org/en/) is a JavaScript runtime environment[^1] based on Google's [Chrome V8](https://developers.google.com/v8/) JavaScript engine and works practically anywhere - from servers to mobile phones
- The code is written into files ending with _.js_ that are run by issuing the command _node name_of_file.js_
- It is also possible to write JavaScript code into the Node.js console, which is opened by typing _node_ in the command line, as well as into the browser's developer tool console. [The newest revisions of Chrome handle the newer features of JavaScript pretty well](https://compat-table.github.io/compat-table/es2016plus/) without transpiling the code. Alternatively, you can use a tool like [JS Bin](https://jsbin.com/?js,console).

### Variables
[What is the difference between var, let, and const - JavaScript](What%20is%20the%20difference%20between%20var,%20let,%20and%20const%20-%20JavaScript.md)
In JavaScript there are a few ways to go about defining variables:

```js
const x = 1
let y = 5

console.log(x, y)   // 1 5 are printed
y += 10
console.log(x, y)   // 1 15 are printed
y = 'sometext'
console.log(x, y)   // 1 sometext are printed
x = 4               // causes an error
```

- [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) does not define a variable but a _constant_ for which the value can no longer be changed. On the other hand, [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) defines a normal variable.
- ** A variable declared with const cannot be reassigned to a different value, the contents of the object it references can still be modified**
- It is also possible to define variables in JavaScript using the keyword [var](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var). For a long time, var was the only way to define variables. The keywords const and let were introduced in 2015 with the release of ES6. In specific situations, var works in a different way compared to variable definitions in most languages - see [JavaScript Variables - Should You Use let, var or const? on Medium](https://medium.com/craft-academy/javascript-variables-should-you-use-let-v
- ar-or-const-394f7645c88f) or [Keyword: var vs. let on JS Tips](http://www.jstips.co/en/javascript/keyword-var-vs-let/) for more information. The use of var is ill-advised and you should stick with using const and let! You can find more on this topic on YouTube - e.g. [var, let and const - ES6 JavaScript Features](https://youtu.be/sjyJBL5fkp8)

### Arrays
```js
const t = [1, -1, 3]

t.push(5) // Adds new item to an Array

console.log(t.length) // 4 is printed
console.log(t[1])     // -1 is printed

t.forEach(value => {
  console.log(value)  // numbers 1, -1, 3, 5 are printed, each on its own line
})                    
```
- `forEach` - One way of iterating through the items of the array is using _forEach_ as seen in the example. _forEach_ receives a _function_ defined using the arrow syntax as a parameter.
- **use Immutable Data structures** - When using React, techniques from functional programming are often used. One characteristic of the functional programming paradigm is the **use of [immutable](https://en.wikipedia.org/wiki/Immutable_object) data structures**.
- **Create New Array** - In React code, it is preferable to use the method [concat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat), which creates a new array with the added item. This ensures the original array remains unchanged.
```js
const t = [1, -1, 3]

const t2 = t.concat(5)  // creates new array

console.log(t)  // [1, -1, 3] is printed
console.log(t2) // [1, -1, 3, 5] is printed
```
- **map( )** - Based on the old array, map creates a _new array_, for which the function given as a parameter is used to create the items.
```js
const t = [1, 2, 3]

const m1 = t.map(value => value * 2)
console.log(m1)   // [2, 4, 6] is printed
```
- Map can also transform the array into something completely different:

```js
const m2 = t.map(value => '<li>' + value + '</li>')
console.log(m2)  
// [ '<li>1</li>', '<li>2</li>', '<li>3</li>' ] is printed
```

- **Array Destructuring** Individual items of an array are easy to assign to variables with the help of the [destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment).

```js
const t = [1, 2, 3, 4, 5]

const [first, second, ...rest] = t

console.log(first, second)  // 1 2 is printed
console.log(rest)          // [3, 4, 5] is printed
```

Above, the variable _first_ is assigned the first integer of the array and the variable _second_ is assigned the second integer of the array. The variable _rest_ "collects" the remaining integers into its own array.

### Objects [^2]
- There are a few different ways of defining objects in JavaScript. One very common method is using [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#Object_literals).
- The properties of an object are referenced by using the "dot" notation, or by using brackets:
- Objects can also be defined using so-called **constructor** functions, which results in a mechanism reminiscent of many other programming languages, e.g. Java's classes. Despite this similarity, JavaScript does not have classes in the same sense as object-oriented programming languages. There has been, however, the addition of the _class syntax_ starting from version ES6, which in some cases helps structure object-oriented classes.

### Functions [^3] [^4]
The complete process, without cutting corners, of defining an arrow function is as follows:

```js
const sum = (p1, p2) => {
  console.log(p1)
  console.log(p2)
  return p1 + p2
}
```

and the function is called as can be expected:

```js
const result = sum(1, 5)
console.log(result)
```

If there is just a single parameter, we can exclude the parentheses from the definition:

```js
const square = p => {
  console.log(p)
  return p * p
}
```

If the function only contains a single expression then the braces are not needed. In this case, the function only returns the result of its only expression. Now, if we remove console printing, we can further shorten the function definition:

```js
const square = p => p * p
```

### Object methods and "this" [^5]
[^6]
Because this course uses a version of React containing React Hooks we do not need to define objects with methods. **The contents of this chapter are not relevant to the course** but are certainly in many ways good to know. In particular, when using older versions of React one must understand the topics of this chapter.

- Arrow functions and functions defined using the _function_ keyword vary substantially when it comes to how they behave with respect to the keyword [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this), which refers to the object itself.
- We can assign methods to an object by defining properties that are functions.
- Let's slightly modify the object:

```js
const arto = {
  name: 'Arto Hellas',
  age: 35,
  education: 'PhD',
  greet: function() {
    console.log('hello, my name is ' + this.name)
  },
  doAddition: function(a, b) {    console.log(a + b)  },}

arto.doAddition(1, 4)        // 5 is printed

const referenceToAddition = arto.doAddition
referenceToAddition(10, 15)   // 25 is printed
```
Now the object has the method `_doAddition_` which calculates the sum of numbers given to it as parameters. The method is called in the usual way, using the object _arto.doAddition(1, 4)_ or by storing a _method reference_ in a variable and calling the method through the variable: _referenceToAddition(10, 15)_.

If we try to do the same with the method _greet_ we run into an issue:
```js
arto.greet()       // "hello, my name is Arto Hellas" gets printed

const referenceToGreet = arto.greet
referenceToGreet() // prints "hello, my name is undefined"
```
When calling the method through a reference, the method loses knowledge of what the original _this_ was. ==Contrary to other languages, in JavaScript the value of [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this) is defined based on _how the method is called_.== When calling the method through a reference, the value of _this_ becomes the so-called [global object](https://developer.mozilla.org/en-US/docs/Glossary/Global_object) and the end result is often not what the software developer had originally intended.

Losing track of _this_ when writing JavaScript code brings forth a few potential issues. Situations often arise where React or Node (or more specifically the JavaScript engine of the web browser) needs to call some method in an object that the developer has defined. However, in this course, we avoid these issues by using "this-less" JavaScript.

One situation leading to the "disappearance" of _this_ arises when we set a timeout to call the _greet_ function on the _arto_ object, using the [setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout) function.

```js
const arto = {
  name: 'Arto Hellas',
  greet: function() {
    console.log('hello, my name is ' + this.name)
  },
}

setTimeout(arto.greet, 1000)
```

There are several mechanisms by which the original _this_ can be preserved. One of these is using a method called [bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind):
```js
setTimeout(arto.greet.bind(arto), 1000)
```
Calling _arto.greet.bind(arto)_ creates a new function where _this_ is bound to point to Arto, independent of where and how the method is being called.

### Classes [^7]
As mentioned previously, there is no class mechanism in JavaScript like the ones in object-oriented programming languages. There are, however, features to make "simulating" object-oriented [classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) possible.


---
## References
[^1](../../What%20is%20a%20Run%20Time%20Environment.md)
[^2](Objects%20-%20Javascript.md)
[^3](Arrow%20Function%20and%20how%20it%20is%20different%20from%20others%20-%20Javascript.md)
[^4](Different%20ways%20to%20define%20or%20declare%20Functions.md)
[^5](this%20-%20Object%20Methods%20in%20Javascript.md)
[^6](Understand%20JavaScript's%20this%20Keyword%20in%20Depth%20-%20Javascript%20)
[^7](Classes%20-%20Javascript.md)