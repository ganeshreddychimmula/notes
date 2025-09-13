
2025-09-13 01:04

Status:

Tags: [JavaScript](../../../3%20-%20Tags/JavaScript.md)

---
# Object.assign() - Javascript
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
The **`Object.assign()`** static method copies all [enumerable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/propertyIsEnumerable) [own properties](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwn) from one or more _source objects_ to a _target object_. It returns the modified target object.

Like spread operator
```js
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// Expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget === target);
// Expected output: true

```

same with spread 
```js
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = {...target, ...source};

console.log(target);
// Expected output: Object { a: 1, b: 2 }

console.log(retunredTarget);
// Expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget === target);
// Expected output: true

```
---
## References