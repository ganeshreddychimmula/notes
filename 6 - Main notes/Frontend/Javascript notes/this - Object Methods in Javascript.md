 
2025-07-14 23:44

Status:

Tags: [JavaScript](3%20-%20Tags/JavaScript.md)

---
# Object methods and this - Javascript


- A function that is property of an object is called "method".
    - **Explanation:** Methods are actions that an object can perform. They are functions defined as properties of an object.
    - **Example:**   
        ```js
        const user = {
            name: "Alice",
            // greet is a method of the user object
            greet: function() {
                console.log("Hello!");
            }
        };
        
        user.greet(); // Calling the method
        ```

### This in javascript
- To access the data of an object, `this` keyword is used.
    - **Explanation:** Inside a method, `this` refers to the object that the method belongs to. This allows the method to access and manipulate the object's properties.
    - **Example:**
        ```js
        const person = {
            name: "Bob",
            age: 30,
            introduce: function() {
                console.log(`Hi, my name is ${this.name} and I am ${this.age} years old.`);
            }
        };
        
        person.introduce(); // Output: Hi, my name is Bob and I am 30 years old.
        ```
        
- In JavaScript, `this` behavior differs. It can be used in any function, even if the function is not a method of an object.
    - ↪️ The value of `this` is evaluated during run-time, based on the context.
        - **Explanation:** Unlike some other languages where `this` is fixed based on where a function is _defined_, in JavaScript, `this` is determined by _how_ the function is called. This dynamic nature is a key aspect of JavaScript.
            
- Calling without assigned to an object: `this === undefined`
    ```js
    'use strict'; // Enable strict mode for predictable 'this' behavior
    
    function sayHi() {
        console.log("Value of 'this':", this);
    }
    sayHi(); // Function called directly, not as a method of an object
    ```
    - ↪️ In this case, `this` is `undefined` in strict mode.
        - **Explanation:** In strict mode, when a function is called directly (not as a method, not with `new`, `call`, `apply`, or `bind`), `this` defaults to `undefined`. This helps prevent accidental global variable creation and makes code more predictable.
    - ↪️ In non-strict mode, the value of `this` in such case will be the global Object (`window` in a browser, or `global` in Node.js).
        - **Explanation:** Historically, in non-strict mode, if `this` wasn't explicitly set, it would fall back to the global object. This behavior is often considered a "mistake" in JavaScript design as it can lead to unintended side effects.
    - ↪️ It's a programming error that can be avoided using strict mode.
        - **Explanation:** Using `'use strict';` at the top of your script or function is highly recommended to enforce stricter parsing and error handling, including the `undefined` behavior for `this` in direct function calls.
            
- In JavaScript, `this` is "free". Its value is evaluated at runtime, and does not depend on where the method is declared, but rather on what object is "before the dot".
    - **Explanation:** This "free" nature means you can define a function once and then attach it as a method to various objects, and `this` will correctly refer to the object it's currently called upon.
    - **Example:**
        ```js
        function showFullName() {
            console.log(`${this.firstName} ${this.lastName}`);
        }
        
        const user1 = {
            firstName: "John",
            lastName: "Doe",
            showName: showFullName // Assigning the function as a method
        };
        
        const user2 = {
            firstName: "Jane",
            lastName: "Smith",
            showName: showFullName // Reusing the same function
        };
        
        user1.showName(); // Output: John Doe (this refers to user1)
        user2.showName(); // Output: Jane Smith (this refers to user2)
        ```
    - ↪️ Benefits:
        - ↪️ Function can be reused on different objects.
        - ↪️ Greater flexibility & possibilities for reuse.
            
- Arrow Functions don't have their own `this`.
    - ↪️ If we reference `this` from such a function, it's taken from the outer normal function (or the surrounding lexical context).
        - **Explanation:** Arrow functions lexically bind `this`. This means they don't create their own `this` context; instead, they inherit `this` from the scope in which they were _defined_. This is often useful for callbacks within methods.
        - **Example:**
            ```js
            const counter = {
                count: 0,
                start: function() {
                    console.log("Regular function 'this':", this); // 'this' is 'counter' object
                    setInterval(() => {
                        // Arrow function: 'this' is inherited from the 'start' method's scope
                        // so 'this' still refers to the 'counter' object.
                        this.count++;
                        console.log(this.count);
                    }, 1000);
                }
            };
            
            // If we used a regular function for the setInterval callback:
            // setInterval(function() {
            //     console.log(this); // 'this' would be the global object (window/undefined in strict mode)
            //     this.count++; // This would cause an error or modify global.count
            // }, 1000);
            
            // counter.start(); // Uncomment to see the counter incrementing
            ```
            
- **Pattern**
    ```js
    'use strict';
    function makeUser() {
        return {
            name: "John",
            ref: this, // 'this' here refers to the context where makeUser() is called
        };
    }
    let user = makeUser();
    // console.log(user.ref.name); // This line will cause an error
    // Output: TypeError: Cannot read properties of undefined (reading 'name')
    ```
- Why did `this` become `undefined`?
    - `makeUser()` is called as a regular function, not as a method (`object.method()`).
        - **Explanation:** When `makeUser()` is invoked as `makeUser()`, there's no "object before the dot." It's a plain function call.
            
    - In strict mode (default mode) `this` inside a regular function is `undefined`.
    - ↪️ Same for non-strict mode (but `this` would be the global object, not `undefined`).
        - **Clarification:** In non-strict mode, `this` would be the global object (`window` in browsers) for a direct function call like `makeUser()`. The original note's "Same for non-strict mode" might be misleading if interpreted as `undefined`. The key is that `this` is _not_ the object being created by `makeUser` in either case.
            
- In JavaScript, the value of `this` depends on how function is called, not where it is defined.
    ```js
    'use strict';
    function makeUser() {
        return {
            name: "John",
            ref() { // This is now a method defined within the object literal
                return this;
            },
        };
    }
    let user = makeUser();
    console.log(user.ref().name); // Output: John
    ```
    - ↪️ Now it worked, because `user.ref()` is a method, and the value of `this` is set to the object `before the dot`.
    - ↪️ `user.ref()` is called as method on `user`.
    - ↪️ When a method is called with the dot syntax (`object.method()`), `this` is set to the object before the dot (`user` in this case).
        - **Explanation:** The crucial difference is that `ref` is now a _method_ of the `user` object. When `user.ref()` is executed, JavaScript automatically sets `this` inside `ref` to `user` because `user` is the object "before the dot" that called the method.

---
## References
[Understand JavaScript's this Keyword in Depth - Javascript ](Understand%20JavaScript's%20this%20Keyword%20in%20Depth%20-%20Javascript%20)