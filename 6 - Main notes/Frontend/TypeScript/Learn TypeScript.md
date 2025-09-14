
2025-09-13 20:31

Status:

Tags: [TypeScript](../../../3%20-%20Tags/TypeScript.md)

---
# TypeScript
https://www.typescriptlang.org/docs/handbook/typescript-from-scratch.html

## TypeScript: A Static Type Checker
Detecting errors in code without running it is referred to as _static checking_. Determining what’s an error and what’s not based on the kinds of values being operated on is known as static _type_ checking.

TypeScript checks a program for errors before execution, and does so based on the _kinds of values_, making it a _static type checker_.

### A Typed Superset of JavaScript
TypeScript is a language that is a _superset_ of JavaScript: JS syntax is therefore legal TS. Syntax refers to the way we write text to form a program. 
<font color="yellow">TypeScript doesn’t consider any JavaScript code to be an error because of its syntax.</font>This means you can take any working JavaScript code and put it in a TypeScript file without worrying about exactly how it is written. <font color="red">However, TypeScript is a _typed_ superset, meaning that it adds rules about how different kinds of values can be used.</font>
#### Types

TypeScript’s type checker is designed to allow correct programs through while still catching as many common errors as possible.

#### Runtime Behavior

TypeScript is also a programming language that preserves the _runtime behavior_ of JavaScript. For example, dividing by zero in JavaScript produces `Infinity` instead of throwing a runtime exception. As a principle, TypeScript **never** changes the runtime behavior of JavaScript code.

Keeping the same runtime behavior as JavaScript is a foundational promise of TypeScript because it means you can easily transition between the two languages without worrying about subtle differences that might make your program stop working.

#### Erased Types

<font color="yellow">Roughly speaking, once TypeScript’s compiler is done with checking your code, it _erases_ the types to produce the resulting “compiled” code. .</font> This means that once your code is compiled, the resulting plain JS code has no type information

This also means that TypeScript never changes the _behavior_ of your program based on the types it inferred. The bottom line is that while you might see type errors during compilation, the type system itself has no bearing on how your program works when it runs.

Finally, TypeScript doesn’t provide any additional runtime libraries. Your programs will use the same standard library (or external libraries) as JavaScript programs, so there’s no additional TypeScript-specific framework to learn.

## Learning JavaScript and TypeScript

 question “Should I learn JavaScript or TypeScript?“.

The answer is that you can’t learn TypeScript without learning JavaScript! TypeScript shares syntax and runtime behavior with JavaScript, so anything you learn about JavaScript is helping you learn TypeScript at the same time.

TypeScript stands in an unusual relationship to JavaScript. TypeScript offers all of JavaScript’s features, and <font color="yellow">an additional layer on top </font>of these: TypeScript’s type system.

This means that your existing working JavaScript code is also TypeScript code. The main benefit of TypeScript is that it can highlight unexpected behavior in your code, lowering the chance of bugs.

## Types by Inference

TypeScript knows the JavaScript language and will generate types for you in many cases.

## Defining Types

You can explicitly describe this object’s shape using an `interface` declaration:

```ts
interface User {

name: string;

id: number;

}
```

You can then declare that a JavaScript object conforms to the shape of your new `interface` by using syntax like `: TypeName` after a variable declaration:

```ts
const user: User = {

name: "Hayes",

id: 0,

};
```

## Composing Types

With TypeScript, you can create complex types by combining simple ones. There are two popular ways to do so: unions and generics.

### Unions

With a union, you can declare that a type could be one of many types. For example, you can describe a `boolean` type as being either `true` or `false`:

```ts
   type MyBool = true | false;   
```
 
A popular use-case for union types is to describe the set of `string` or `number` [literals](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-types) that a value is allowed to be.

To learn the type of a variable, use `typeof`

### Generics

Generics provide variables to types. A common example is an array. An array without generics could contain anything. An array with generics can describe the values that the array contains.

```ts
type StringArray = Array<string>;

type NumberArray = Array<number>;

type ObjectWithNameArray = Array<{ name: string }>;
```

You can declare your own types that use generics:
```ts
interface Backpack<Type> {

add: (obj: Type) => void;

get: () => Type;

}

// This line is a shortcut to tell TypeScript there is a

// constant called `backpack`, and to not worry about where it came from.

declare const backpack: Backpack<string>;

// object is a string, because we declared it above as the variable part of Backpack.

const object = backpack.get();

// Since the backpack variable is a string, you can't pass a number to the add function.

backpack.add(23);
`Warning: Argument of type 'number' is not assignable to parameter of type 'string'.`
```


## Structural Type System

One of TypeScript’s core principles is that type checking focuses on the _shape_ that values have. This is sometimes called “duck typing” or “structural typing”.

In a structural type system, if two objects have the same shape, they are considered to be of the same type.

```ts
interface Point {

x: number;

y: number;

}

function logPoint(p: Point) {

console.log(`${p.x}, ${p.y}`);

}

// logs "12, 26"

const point = { x: 12, y: 26 };

logPoint(point);
```

The `point` variable is never declared to be a `Point` type. However, TypeScript compares the shape of `point` to the shape of `Point` in the type-check. They have the same shape, so the code passes.

The shape-matching only requires a subset of the object’s fields to match.

```ts
const point3 = { x: 12, y: 26, z: 89 };

logPoint(point3); // logs "12, 26"

const rect = { x: 33, y: 3, width: 30, height: 80 };

logPoint(rect); // logs "33, 3"

const color = { hex: "#187ABF" };

logPoint(color);
// Argument of type '{ hex: string; }' is not assignable to parameter of type 'Point'. Type '{ hex: string; }' is missing the following properties from type 'Point': x, y
```

---
## References