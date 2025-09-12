
2025-09-12 13:24

Status:

Tags:

---
# Typescript Course - Scrimba

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

- 
---
## References