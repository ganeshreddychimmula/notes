
2025-09-12 13:24

Status:

Tags:

---
# Typescript Course - Scrimba
https://www.typescriptlang.org/docs/handbook/typescript-from-scratch.html
- Setting up typescript
- Typescript inherently makes us think of Fail safes and edge cases that we usually have be pretty conscious of.
- Primitive types declaration
```tsx
let myName: string = "Bob"
  
let numberOfWheels: number = 4

let isStudent: boolean = false
```

- Custom types
	- `type` Keyword
```ts
type Pizza = {
    name: string
    price: number
}
type Person = {
    name: string
    age: number
    isStudent: boolean
    address: {
        street: string
        city: string
        country: string
    }
    pizza: Pizza
}
```

- Relaxing rigidity using optional args
```ts
type Person = {

    name: string

    age: number

    isStudent: boolean

    address?: Address

}
```

 -  Typing Arrays
 `let people: Person[] = [person1, person2]`

- literal types
```jsx
let myName: "Bob" = "Bob"
const myName2: "Bob" = "Bob" // You don't need to declare such types, because typescript automatically infers these
```

- Unions
`type UserRole = "guest" | "member" | "admin"`
- Type Narrowing
![](../../../2%20-%20Source%20Material/Media%20and%20other%20files/Pasted%20image%2020250913001823.png)
- Function return types
```ts
function fetchUserDetails(username: string): User {

    const user = users.find(user => user.username === username)

    if (!user) {

        throw new Error(`User with username ${username} not found`)

    }

    return user

}
```

- `void` return type
```ts
function addNewPizza(pizzaObj: Pizza): void {

    menu.push(pizzaObj)

}
```

- TypeScript specific types
	- `any` - like disabling type checking
	- Avoid using  `any`
- Utility Types
	- https://www.typescriptlang.org/docs/handbook/utility-types.html#partialtype
	-  Like a function, they take other types in as a parameter and return a new type, with some changes made to it
	- Built-in to typescript; perform commonly needed modifications to existing types
	- They use "Generics" syntax using angle brackets(<>)
	- `Partial<Type>` - a utility type that Constructs a type with all properties of `Type` set to optional. This utility will return a type that represents all subsets of a given type.

```js
type User = {

    id?: number

    username?: string

    role?: "member" | "contributor" | "admin"

}

type UpdatedUser = {

    id?: number

    username?: string

    role?: "member" | "contributor" | "admin"

}

// Partial<User> === updatedUser
function updateUser(id: number, updates: Partial<User>) {

    // Find the user in the array by the id

    const foundUser = users.find(user => user.id === id)

    if (!foundUser) {

        console.error("User not found!")

        return

    }

    // Use Object.assign to update the found user in place.

    Object.assign(foundUser, updates)

}

updateUser(id: nextUserId++; {name: "something", role:"memnber"})

//Better Alternative : Omit<Type, keys>
function addNewPizza(pizzaObj: Pizza): void {

    pizzaObj.id = nextPizzaId++

    menu.push(pizzaObj)

}

addNewPizza({ name: "Chicken Bacon Ranch", price: 12 })

addNewPizza({ name: "BBQ Chicken", price: 12 })

addNewPizza({ name: "Spicy Sausage", price: 11 })
```

- Generics
	- https://www.typescriptlang.org/docs/handbook/2/generics.html
	- Add flexibility to existing functions, types, etc.
	- Act like function parameters, but for types
	- use angle bracket syntax(<>)
```ts
// <T> is popular alternative for type, but use can use anything there


const gameScores = [14, 21, 33, 42, 59]

const favoriteThings = ["raindrops on roses", "whiskers on kittens", "bright copper kettles", "warm woolen mittens"];

const voters = [{ name: "Alice", age: 42 }, { name: "Bob", age: 77 }]

function getLastItem<T>(array: T) {

    return array[array.length - 1]

}  

function getLastItem<PlaceholderType>(array: PlaceholderType[]): PlaceholderType {

    return array[array.length - 1]

}

console.log(getLastItem<string>(favoriteThings))

console.log(getLastItem<number>(gameScores))
  

console.log(getLastItem<string>(favoriteThings))

console.log(getLastItem<number>(gameScores))

console.log(getLastItem<{

    name: string;

    age: number;

}>(voters))
```

---
## References

[Typescript in React - Scrimba](Typescript%20in%20React%20-%20Scrimba.md)
