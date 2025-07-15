
2025-07-14 23:12

Status:

Tags: [[JavaScript]]

---
# Objects - Javascript
### Objects

- Creating an Object:
    
    - `let user = new Object();` // Object "constructor" syntax
        
    - `let user = {};` // Object "literal" syntax
        
- In JavaScript, an object is a collection of key-value pairs.
    
    - where keys (also called "properties") are strings (or symbols)
        
    - & values can be any datatype, including other objects & functions.
        
- To remove a property:
    
    - `delete user.age`
        
- multiword property names must be quoted.
    
    ```
    let user = {
        name: "John",
        "likes birds": true,
    };
    ```
    
- last line in property list and with comma
    

### Computed properties in an object

- For multi-word properties, use square brackets to access:
    
    - `user["like words"] = true;`
        
- Computed properties in JavaScript allow you to dynamically set object keys using expressions, rather than static.
    
    - ↪️ & this is useful when you want the property name to be determined at runtime.
        
- you define computed properties by enclosing an expression inside square brackets `[]` when defining an object.
    
    ```
    const keyName = "age";
    const person = {
        name: "Alice",
        [keyName]: 25 // computed property
    };
    ```
    
    - ↪️ here the `keyName` ("age") is used as the property name.
        

### Computed properties are useful when you need flexibility in defining object keys dynamically. Some of their popular uses cases are:

1. Handling user-generated property names.
    
2. Creating objects in loops.
    
3. Using dynamic keys from external resources (like APIs).
    

### Property name shorthand

```
name: "hello";
let myObject = {
    name, // method of name: name,
    age: 30,
};
```

### Property name limitations

- For object property names there are no limitations like the use of reserved keywords, which are applicable to regular variable naming.
    
- ↪️ You can also use properties that start with numbers.
    

**Note**: we can't set `__proto__` to a non-object value.

### Property order in objects

1. Numeric properties first (sorted in Ascending order)
    
2. String properties (insertion order)
    
    - ↪️ Any non-numeric string keys appear in the order they were inserted.
        
3. Symbol properties (insertion order)
    
    - ↪️ after string properties.
        

### "in" operator, property existence test

- In JavaScript, it is okay to access any property even if it doesn't exist, it doesn't throw an error.
    
- Reading a non-existent property returns `undefined`.
    
    ```
    let user = {};
    user.age === undefined //true
    ```
    
    - ↪️ or we can use "in" operator.
        
    
    ```
    "age" in user // false
    ```
    

### The "for...in" loop

- To work over all keys of an object, there exists a special form of the loop: `for...in`
    
    ```
    for (let key in user) {
        console.log(user[key]);
    }
    ```

### Object - Garbage Collection

- In JavaScript, reachability refers to whether an object is accessible (or reachable) from the root of execution, which prevents it being garbage collected.
    
- If an object is no longer referenced, it becomes unreachable and is eligible for garbage collection.
    
- outgoing references do not matter. Only incoming ones can make an object reachable.
    
- The basic garbage collection algorithm is called mark-and-sweep.
    
- Garbage collection is performed automatically. We cannot force or prevent it.
    

---
## References
[[Referencing, copying, cloning and merging an Object - Javascript]]
[[this - Object Methods in Javascript]]