
2025-07-14 23:30

Status:

Tags:

---
# Referencing, copying, cloning and merging an Object - Javascript
## Object references and Copying

- Difference between Object versus primitive
    - Objects are stored and copied by "reference"
        - **Explanation:** When you assign an object to a variable or pass it to a function, you're not copying the entire object. Instead, you're copying a "pointer" or "reference" to where that object lives in memory.
        - **Example:**
            
            ```js
            let obj1 = { value: 10 };
            let obj2 = obj1; // obj2 now references the *same* object as obj1
            
            obj2.value = 20; // Modifying obj2 also modifies obj1 because they point to the same object
            
            console.log(obj1.value); // Output: 20
            console.log(obj1 === obj2); // Output: true (They are the exact same object in memory)
            ```
            
    - Primitives (strings, number, boolean, null, undefined, symbol, bigint) are always copied as a whole (by "value").
        - **Explanation:** When you assign a primitive value to a variable or pass it around, a completely independent copy of that value is made. Changes to the copy do not affect the original.
        - **Example:**
            ```
            let num1 = 10;
            let num2 = num1; // num2 gets a *copy* of the value 10
            
            num2 = 20; // Modifying num2 does not affect num1
            
            console.log(num1); // Output: 10
            console.log(num1 === num2); // Output: false
            ```
            
- A variable assigned to an object stores not the object itself, but its "address in memory" - in other words "a reference" to it.
    - **Analogy:** Imagine a library. Instead of giving you the entire book, the librarian gives you a slip of paper with the book's shelf number and position. This slip of paper is the "reference." If someone else also gets a slip for the same book, both slips point to the _one_ physical book.
        
- When an object variable is copied, the reference is copied, but the object itself is not duplicated.
    - **Example:**
        ```
        let car1 = { make: 'Toyota', model: 'Camry' };
        let car2 = car1; // car2 now holds the *same reference* as car1
        
        console.log(car1); // { make: 'Toyota', model: 'Camry' }
        console.log(car2); // { make: 'Toyota', model: 'Camry' }
        
        car2.model = 'Corolla'; // We modified the object *through* car2's reference
        
        console.log(car1.model); // Output: 'Corolla' (car1 also sees the change)
        console.log(car1 === car2); // Output: true (They refer to the identical object)
        ```
        
- So, two independently created objects are not equal even though they end up looking alike.
    - **Explanation:** The `===` (strict equality) operator for objects checks if two variables refer to the _exact same object in memory_, not if their contents are identical.
    - **Example:**
        ```
        let person1 = { name: 'Alice', age: 30 };
        let person2 = { name: 'Alice', age: 30 }; // A new, separate object is created
        
        console.log(person1 === person2); // Output: false
        // Even though they have the same properties and values, they are distinct objects
        // residing at different memory addresses.
        ```
        
- An important side-effect of storing objects as reference is that an object declared as `const` can be modified.
    - ↪️ Properties can be modified
        - **Explanation:** The `const` keyword prevents reassignment of the variable itself. For objects, this means the variable will _always_ point to the _same memory address_. However, the _contents_ of the object at that memory address can still be changed.
        - **Example:**
            ```
            const settings = { theme: 'dark', notifications: true };
            
            // This is allowed: modifying properties of the object
            settings.theme = 'light';
            settings.notifications = false;
            
            console.log(settings); // Output: { theme: 'light', notifications: false }
            ```
            
    
    - ↪️ The reference itself or object as a whole can't be modified.
        - **Explanation:** You cannot make the `const` variable point to a _different_ object after its initial assignment.
        - **Example:**
            ```
            const user = { id: 1, name: 'Bob' };
            
            // This will cause an error:
            // TypeError: Assignment to constant variable.
            // user = { id: 2, name: 'Charlie' };
            
            console.log(user); // Still { id: 1, name: 'Bob' } (if error is caught/ignored)
            ```
            

### Additional Relevant Concepts

- **Pass by Value vs. Pass by Reference in Functions**
    - **Explanation:** This concept directly relates to how arguments are handled when passed to functions, building upon the understanding of primitives vs. objects.
        
    - **Primitives (Pass by Value):** When a primitive value is passed to a function, a _copy_ of that value is made for the function's parameter. Changes to the parameter inside the function do not affect the original variable outside.
        - **Example:**
            ```
            function increment(num) {
                num = num + 1;
                console.log("Inside function (num):", num); // Output: 11
            }
            
            let myNumber = 10;
            increment(myNumber);
            console.log("Outside function (myNumber):", myNumber); // Output: 10 (Original unchanged)
            ```
            
    - **Objects (Pass by Reference):** When an object is passed to a function, a _copy of the reference_ to that object is made for the function's parameter. Both the original variable and the function parameter point to the _same object_ in memory. Therefore, changes made to the object _through the parameter_ inside the function will affect the original object outside.
        - **Example:**
            ```
            function changeName(personObj) {
                personObj.name = "Jane Doe";
                console.log("Inside function (personObj):", personObj); // Output: { name: 'Jane Doe', age: 25 }
            }
            
            let myPerson = { name: "John Doe", age: 25 };
            changeName(myPerson);
            console.log("Outside function (myPerson):", myPerson); // Output: { name: 'Jane Doe', age: 25 } (Original changed)
            ```
            
        - **Important Note:** While the _object's properties_ can be changed, the function cannot reassign the original variable to a _new object_ because it only has a copy of the reference.
            ```
            function tryReassign(obj) {
                obj = { newValue: 100 }; // Reassigns the local parameter 'obj', not the original variable
                console.log("Inside function (reassigned obj):", obj); // Output: { newValue: 100 }
            }
            
            let originalObj = { old: 50 };
            tryReassign(originalObj);
            console.log("Outside function (originalObj):", originalObj); // Output: { old: 50 } (Original unchanged)
            ```
            
- **Immutability**
    - **Explanation:** Immutability means that once an object is created, its state cannot be changed. Instead of modifying an existing object, you create a new object with the desired changes. This is a common pattern in functional programming and React to prevent unexpected side effects and make state management more predictable.
        
    - **Why it's relevant:** Understanding object references is crucial for practicing immutability. To achieve immutability, you often need to perform shallow or deep copies to create new objects rather than mutating existing ones.
    - **Example (Immutability with spread operator for shallow copy):**
        
        ```
        const userProfile = {
            id: 1,
            name: 'Alice',
            settings: { theme: 'dark' }
        };
        
        // To change the theme immutably, create new objects at each level
        const updatedUserProfile = {
            ...userProfile, // Copy top-level properties
            settings: {
                ...userProfile.settings, // Copy nested settings properties
                theme: 'light' // Update the theme
            }
        };
        
        console.log(userProfile.settings.theme);       // Output: 'dark' (Original unchanged)
        console.log(updatedUserProfile.settings.theme); // Output: 'light' (New object has updated theme)
        console.log(userProfile === updatedUserProfile); // Output: false
        console.log(userProfile.settings === updatedUserProfile.settings); // Output: false (Nested object also new)
        ```
        
- **`Object.freeze()`**
    
    - **Explanation:** `Object.freeze()` is a method that makes an object immutable at its top level. It prevents new properties from being added to it, existing properties from being removed, and existing properties (including their enumerability, configurability, and writability) from being changed.
        
    - **Relevance:** While `const` prevents reassignment of the variable, `Object.freeze()` prevents modification of the object's properties. It's a way to enforce a higher level of immutability.
        
    - **Important Caveat:** `Object.freeze()` performs a _shallow_ freeze. If the object contains other objects, those nested objects are _not_ frozen and can still be modified. For a deep freeze, you would need a recursive function.
        
    - **Example:**
        
        ```
        const immutableConfig = {
            version: '1.0',
            features: {
                darkMode: true,
                notifications: false
            }
        };
        
        Object.freeze(immutableConfig); // Freeze the top-level object
        Object.freeze(immutableConfig.features); // Manually freeze nested objects for deep immutability
        
        try {
            immutableConfig.version = '1.1'; // This will fail silently in non-strict mode, or throw TypeError in strict mode
            immutableConfig.newProp = 'value'; // This will fail silently or throw TypeError
            immutableConfig.features.darkMode = false; // This will also fail if features was frozen
        } catch (e) {
            console.error("Error modifying frozen object:", e.message);
        }
        
        console.log(immutableConfig);
        // Output: { version: '1.0', features: { darkMode: true, notifications: false } } (unchanged)
        ```
## Cloning and merging Objects

1. **Shallow Copy**
    
    - A shallow copy creates a new object with the same properties, but nested objects or arrays are still references.
        
        - **Explanation:** Think of it like making a new folder (the new object) and putting shortcuts (references) to the original files (nested objects/arrays) inside it, rather than making copies of the files themselves. If you change the original file, the shortcut in the new folder will reflect that change.
            
    - Using `Object.assign()`
        
        ```
        const obj = { a: 1, b: { c: 2 } };
        const copy = Object.assign({}, obj);
        
        console.log(copy); // Output: { a: 1, b: { c: 2 } }
        
        // Modify the nested object in the copy
        copy.b.c = 3;
        
        console.log(copy.b.c); // Output: 3
        console.log(obj.b.c);  // Output: 3 (Original also changed because 'b' is a shared reference)
        console.log(obj === copy); // Output: false (The top-level objects are different)
        console.log(obj.b === copy.b); // Output: true (The nested object 'b' is the same reference)
        ```
        
        - Problem: nested objects still share references.
            
            - ↪️ In the above example, `{c: 2}` still has same reference, not cloned.
                
    - Using spread operator (`...obj`)
        
        ```
        const originalArray = [1, { value: 'a' }, 3];
        const shallowCopyArray = [...originalArray];
        
        console.log(shallowCopyArray); // Output: [1, { value: 'a' }, 3]
        
        shallowCopyArray[1].value = 'b'; // Modify the nested object in the copy
        
        console.log(shallowCopyArray[1].value); // Output: 'b'
        console.log(originalArray[1].value);    // Output: 'b' (Original also changed)
        console.log(originalArray === shallowCopyArray); // Output: false
        console.log(originalArray[1] === shallowCopyArray[1]); // Output: true
        
        const originalObject = { name: 'Alice', details: { age: 30 } };
        const shallowCopyObject = { ...originalObject };
        
        console.log(shallowCopyObject); // Output: { name: 'Alice', details: { age: 30 } }
        
        shallowCopyObject.details.age = 31; // Modify nested object
        
        console.log(shallowCopyObject.details.age); // Output: 31
        console.log(originalObject.details.age);    // Output: 31 (Original also changed)
        console.log(originalObject === shallowCopyObject); // Output: false
        console.log(originalObject.details === shallowCopyObject.details); // Output: true
        ```
        
        - ↪️ doesn't clone deeply
            
2. **Deep copy**
    
    - A deep copy creates a completely independent copy, including all the nested objects.
        
        - **Explanation:** This is like making a new folder and then making _actual copies_ of all the files inside it, including files within subfolders. Any changes to the new copies won't affect the originals.
            
    - Using `JSON.parse(JSON.stringify(obj))`
        
        ```
        const obj = { a: 1, b: { c: 2 }, d: [4, 5] };
        const deepCopy = JSON.parse(JSON.stringify(obj));
        
        console.log(deepCopy); // Output: { a: 1, b: { c: 2 }, d: [4, 5] }
        
        deepCopy.b.c = 10;
        deepCopy.d[0] = 20;
        
        console.log(deepCopy.b.c); // Output: 10
        console.log(obj.b.c);      // Output: 2 (Original is unchanged)
        console.log(deepCopy.d[0]); // Output: 20
        console.log(obj.d[0]);      // Output: 4 (Original is unchanged)
        console.log(obj.b === deepCopy.b); // Output: false (Nested object 'b' is a new reference)
        console.log(obj.d === deepCopy.d); // Output: false (Nested array 'd' is a new reference)
        ```
        
        - ↪️ simple & works well with plain objects & arrays
            
        - Cons:
            
            - ↪️ loses functions, Date, Map, Set, Symbol & undefined.
                
                - **Example of data loss:**
                    
                    ```
                    const complexObj = {
                        name: 'Test',
                        date: new Date(),
                        func: () => console.log('hello'),
                        sym: Symbol('id'),
                        undef: undefined,
                        map: new Map([[1, 'one']])
                    };
                    const deepCopyBroken = JSON.parse(JSON.stringify(complexObj));
                    
                    console.log(deepCopyBroken.date); // Output: "2025-07-14T..." (string, not Date object)
                    console.log(deepCopyBroken.func); // Output: undefined (function lost)
                    console.log(deepCopyBroken.sym);  // Output: undefined (Symbol lost)
                    console.log(deepCopyBroken.undef); // Output: undefined (undefined property lost)
                    console.log(deepCopyBroken.map);  // Output: {} (Map converted to empty object)
                    ```
                    
            - ↪️ Can fail for circular references.
                
                - **Example of circular reference failure:**
                    
                    ```
                    const circularObj = {};
                    circularObj.self = circularObj; // circular reference
                    
                    try {
                        JSON.parse(JSON.stringify(circularObj));
                    } catch (e) {
                        console.error("Error:", e.message); // Output: "Converting circular structure to JSON"
                    }
                    ```
                    
    - Using `structuredClone(obj)` (Modern approach)
        
        ```
        const obj = {
            a: 1,
            b: { c: 2 },
            d: new Date(),
            e: new Map([[1, 'one']]),
            f: new Set([1, 2])
        };
        const deepCopy = structuredClone(obj);
        
        console.log(deepCopy);
        // Output: { a: 1, b: { c: 2 }, d: Date object, e: Map object, f: Set object }
        
        deepCopy.b.c = 100;
        deepCopy.d.setFullYear(2030);
        deepCopy.e.set(2, 'two');
        
        console.log(obj.b.c); // Output: 2 (Original unchanged)
        console.log(obj.d.getFullYear()); // Output: 2025 (Original unchanged)
        console.log(obj.e.get(2)); // Output: undefined (Original Map unchanged)
        ```
        
        - Drawbacks:
            
            - ↪️ Not available in older browsers (Only modern browsers & Node.js 17+)
                
            - ↪️ Functional properties aren't supported.
                
                - **Explanation:** `structuredClone` is designed for "structured data" and will throw an error if you try to clone objects containing functions, DOM nodes, or certain other non-serializable types.
                    
    - Using Lodash (`_.cloneDeep`)
        
        - Requires `lodash`.
            
            - **Installation (if using Node.js/npm):** `npm install lodash`
                
            - **Import (if using ES Modules):** `import _ from 'lodash';`
                
            - **Import (if using CommonJS):** `const _ = require('lodash');`
                
            - **Via CDN (for browser):** `<script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>`
                
        
        ```
        // Assuming Lodash is available (e.g., via CDN or import)
        const obj = {
            a: 1,
            b: { c: 2 },
            d: new Date(),
            e: new Map([[1, 'one']]),
            f: () => console.log('hello'),
            g: null
        };
        const deepCopy = _.cloneDeep(obj);
        
        console.log(deepCopy);
        // Output: { a: 1, b: { c: 2 }, d: Date object, e: Map object, f: [Function: f], g: null }
        
        deepCopy.b.c = 50;
        console.log(obj.b.c); // Output: 2 (Original unchanged)
        deepCopy.f(); // Function is copied and callable
        ```
        
        - Drawbacks:
            
            - ↪️ requires external library.
                
    - You can deep copy manually using recursive function.
        
        - **Explanation:** This involves writing a function that iterates over an object's properties. If a property's value is an object (and not `null`), the function calls itself recursively on that nested object. Primitive values are copied directly. This gives you the most control but is more complex to implement correctly for all edge cases.
            
        
        ```
        function deepClone(obj) {
            if (obj === null || typeof obj !== 'object') {
                return obj; // Return primitive values directly
            }
        
            // Handle Date objects
            if (obj instanceof Date) {
                return new Date(obj.getTime());
            }
        
            // Handle Array objects
            if (Array.isArray(obj)) {
                return obj.map(item => deepClone(item));
            }
        
            // Handle plain objects
            const clonedObj = {};
            for (const key in obj) {
                if (Object.prototype.hasOwnProperty.call(obj, key)) {
                    clonedObj[key] = deepClone(obj[key]);
                }
            }
            return clonedObj;
        }
        
        const original = {
            name: 'John',
            address: {
                street: '123 Main St',
                city: 'Anytown'
            },
            hobbies: ['reading', 'coding'],
            birthDate: new Date('1990-01-01')
        };
        
        const cloned = deepClone(original);
        
        console.log(cloned);
        // Output: { name: 'John', address: { street: '123 Main St', city: 'Anytown' }, hobbies: ['reading', 'coding'], birthDate: Date object }
        
        cloned.address.city = 'Newtown';
        cloned.hobbies.push('hiking');
        cloned.birthDate.setFullYear(1995);
        
        console.log(original.address.city); // Output: Anytown (Original unchanged)
        console.log(original.hobbies);      // Output: ['reading', 'coding'] (Original unchanged)
        console.log(original.birthDate.getFullYear()); // Output: 1990 (Original unchanged)
        ```

---
## References