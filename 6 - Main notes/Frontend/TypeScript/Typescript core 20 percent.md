
2025-09-12 12:42

Status:

Tags: [TypeScript](../../../3%20-%20Tags/TypeScript.md)

---
# Typescript core 20 percent

 Here are the core topics to master for maximum impact.

---

### ## 1. The Fundamentals of Type Annotation

This is the absolute foundation. Understanding how to add types to your JavaScript code is the most critical skill.

- **Basic Types:** Focus on annotating primitive types: `string`, `number`, `boolean`, `null`, and `undefined`.
    
- **Arrays and Objects:** Learn the syntax for typing arrays (`string[]` or `Array<string>`) and basic objects (`{ name: string; age: number }`).
    
- **Type Inference:** Understand that TypeScript often knows the type of a variable without you explicitly writing it. Rely on this to keep your code clean. For example, `let name = 'Alice';` is automatically inferred as `string`.
    

---

### ## 2. Typing Functions

Functions are the workhorses of any application. Knowing how to type them correctly prevents a massive number of common bugs.

- **Parameter Types:** Define the expected types for function arguments (`function greet(name: string) { ... }`).
    
- **Return Types:** Specify what type of value a function returns (`function getAge(): number { return 25; }`). TypeScript can often infer this, but being explicit is good practice for clarity.
    

---

### ## 3. Shaping Data with `type` and `interface`

You'll constantly need to define the "shape" of objects and other complex data structures. `type` aliases and `interface` are how you do it.

- **`type` Aliases:** Create custom names for any type, which is great for unions or complex object shapes.
    
    - Example: `type UserID = string | number;`
        
- **`interface`:** The primary way to define the structure of an object.
    
    - Example:
        
        TypeScript
        
        ```
        interface User {
          id: UserID;
          username: string;
          isActive: boolean;
        }
        ```
        

For most day-to-day use cases, `type` and `interface` are largely interchangeable for defining objects. Just pick one and be consistent.

---

### ## 4. Combining Types with Union and Intersection

This is how you create flexible and realistic types that match real-world data.

- **Union Types (`|`):** Used when a value can be one of **several** types. The pipe character `|` acts like an "OR". This is extremely common for function parameters or API responses.
    
    - Example: `let id: string | number;` means `id` can be a string _or_ a number.
        
- **Intersection Types (`&`):** Used to combine multiple types into one. The ampersand `&` acts like an "AND".
    
    - Example: `type Employee = User & { department: string; };` creates a new type that has all properties of `User` _and_ a `department` property.
        

---

### ## 5. Generics: Creating Reusable, Type-Safe Code

Generics are arguably the most powerful feature for an intermediate developer. They allow you to write functions and components that can work over a **variety of types** rather than a single one, while preserving type information. 📦

- **Core Concept:** Think of generics as passing a type as a variable to a function or class. The most common syntax uses `<T>` as a placeholder for the type.
    
- **Practical Example:** A function that takes an array of _any_ type and returns the first element, without losing its type information.
    
    TypeScript
    
    ```
    function getFirstElement<T>(arr: T[]): T | undefined {
      return arr[0];
    }
    
    const firstString = getFirstElement(['a', 'b', 'c']); // Type is 'string'
    const firstNumber = getFirstElement([1, 2, 3]);       // Type is 'number'
    ```
    

By focusing on these five areas, you'll gain the skills needed to handle the vast majority of tasks you'll encounter while writing modern, type-safe applications.

---
## References