
2025-07-15 16:44

Status:

Tags:

---
# Prototypal inheritance - Javascript
### Prototypal Inheritance

- Prototypal Inheritance
    
    - ↪️ It helps us inherit properties & methods from one object to one or more objects.
        
    - **Explanation:** Instead of classes, JavaScript uses prototypes for inheritance. Objects can inherit properties and methods directly from other objects. This creates a "chain" where if a property isn't found on an object, JavaScript looks it up on that object's prototype, then that prototype's prototype, and so on, until it finds the property or reaches `null`.
        
- `[Prototype](Prototype)`
    
    - In JS, objects have a hidden property `[Prototype](Prototype)` that is either `null` or references another object.
        
    - ↪️ That object is called a "prototype".
        
    
    ```
    graph LR
        A[myObject] --> B[myObject's prototype]
        A -- [Prototype](Prototype) --> B
        B --> C[myObject's prototype's prototype]
        C --> D[null]
    ```
    
- When we read a property from the object & it's missing, JavaScript automatically takes it from the prototype.
    
    - ↪️ This is called "prototypal Inheritance".
        
    - **Example:**
        
        ```
        const animal = {
            eats: true,
            walk() {
                console.log("Animal walks.");
            }
        };
        
        const rabbit = {
            jumps: true
        };
        
        // Set animal as the prototype of rabbit
        Object.setPrototypeOf(rabbit, animal); // Modern way to set [Prototype](Prototype)
        
        console.log(rabbit.eats); // Output: true (inherited from animal)
        rabbit.walk();            // Output: Animal walks. (inherited method)
        console.log(rabbit.jumps); // Output: true (own property)
        ```
        
- The property `[Prototype](Prototype)` is internal and hidden, but there are many ways to set it.
    
- `__proto__`
    
    - `obj2.__proto__ = obj1`
        
        - ↪️ `obj1` is prototype of `obj2`.
            
        - ↪️ `obj2` prototypically inherits `obj1`.
            
    - **Explanation:** `__proto__` is a legacy (but still widely supported) getter/setter for the `[Prototype](Prototype)` internal property. While convenient for examples, `Object.setPrototypeOf()` or `Object.create()` are generally preferred for setting prototypes in production code.
        
    - **Example:**
        
        ```
        const vehicle = {
            wheels: 4,
            drive() {
                console.log("Driving a vehicle.");
            }
        };
        
        const car = {
            brand: "Toyota"
        };
        
        car.__proto__ = vehicle; // Set vehicle as prototype of car
        
        console.log(car.wheels); // Output: 4 (inherited from vehicle)
        car.drive();             // Output: Driving a vehicle. (inherited method)
        ```
        
- There are only 2 limitations:
    
    - The references can't go in circle - JavaScript will throw an error if we try to assign `__proto__` in a circle.
        
        - **Example:**
            
            ```
            let a = {};
            let b = {};
            a.__proto__ = b;
            try {
                b.__proto__ = a; // Throws: TypeError: Cyclic __proto__ value
            } catch (e) {
                console.error("Error:", e.message);
            }
            ```
            
    - The value of `__proto__` can either be an object or `null`. Other types are ignored.
        
        - **Example:**
            
            ```
            let obj = {};
            obj.__proto__ = 123; // Primitive value, ignored
            console.log(Object.getPrototypeOf(obj)); // Output: [Object: null prototype] {} (still inherits from Object.prototype)
            
            obj.__proto__ = "string"; // String value, ignored
            console.log(Object.getPrototypeOf(obj)); // Output: [Object: null prototype] {}
            ```
            
- There may be only one `[prototype](prototype)`. An object may not prototypically inherit from two other objects.
    
    - **Explanation:** JavaScript's prototypal inheritance is a single-parent inheritance model. An object can only have one direct prototype. However, this prototype can itself have a prototype, forming a chain.
        
- `__proto__` is getter/setter for `[prototype](prototype)` (old).
    
    - **Explanation:** It's considered a deprecated feature for direct use in new code, but it's still widely supported by browsers and Node.js. `Object.getPrototypeOf()` and `Object.setPrototypeOf()` are the modern alternatives.
        

### Read vs Write in Prototypal Inheritance

- **Read (`this.someProperty`)**
    
    - ↪️ If `someProperty` is not found on the object, JS looks up prototype chain & reads from there.
        
    - **Example:**
        
        ```js
        const head = {
            glasses: true
        };
        const table = {
            pen: true,
            __proto__: head // table inherits from head
        };
        const bed = {
            sheet: true,
            __proto__: table // bed inherits from table
        };
        
        console.log(bed.glasses); // Output: true (found on head, via table)
        console.log(bed.pen);     // Output: true (found on table)
        console.log(bed.sheet);   // Output: true (found on bed itself)
        ```
        
- **Write (`this.someProperty = value`)**
    
    - ↪️ If `someProperty` already exists in Object: Update
        
        - **Example:**
            
            ```js
            const parent = { value: 10 };
            const child = { __proto__: parent, value: 20 }; // child has its own 'value'
            
            child.value = 30; // Updates child's own 'value' property
            console.log(child.value);  // Output: 30
            console.log(parent.value); // Output: 10 (parent's value is unchanged)
            ```
            
    - ↪️ If `someProperty` does not exist on the object but exists in prototype chain:
        
        - ↪️ If its primitive (string, number, boolean) -> does not modify the prototype, instead, it creates a new property on Object.
            
            - **Example:**
                
                ```js
                const protoObj = { count: 0 };
                const myObj = { __proto__: protoObj };
                
                console.log(myObj.count); // Output: 0 (reads from protoObj)
                
                myObj.count = 5; // 'count' doesn't exist on myObj, so a new 'count' property is created on myObj
                console.log(myObj.count);    // Output: 5 (reads from myObj)
                console.log(protoObj.count); // Output: 0 (protoObj's 'count' is unchanged)
                ```
                
        - ↪️ If it's an object (Canvas, object, function) -> The reference is shared, so changes affect the prototype.
            
            - **Explanation:** This is a common pitfall. If a property on the prototype is an object (like an array or another object), and you modify _its contents_ (e.g., push to an array, change a nested property), you are modifying the _shared object_ on the prototype, which affects all objects that inherit from it.
                
            - **Example:**
                
                ```js
                const protoConfig = {
                    settings: {
                        theme: 'dark',
                        notifications: true
                    },
                    items: [1, 2]
                };
                const instance1 = { __proto__: protoConfig };
                const instance2 = { __proto__: protoConfig };
                
                // Modifying a nested object property (shared reference)
                instance1.settings.theme = 'light';
                console.log(instance2.settings.theme); // Output: 'light' (instance2 also sees the change!)
                
                // Modifying a nested array (shared reference)
                instance1.items.push(3);
                console.log(instance2.items); // Output: [1, 2, 3] (instance2 also sees the change!)
                
                // To avoid this, you'd need to create a new object/array on the instance first:
                // instance1.settings = { ...instance1.settings, theme: 'light' }; // Creates new settings object for instance1
                ```
                
- `prototype` is only used for reading properties. Write/delete operations work directly with the object.
    
    - **Explanation:** When you assign a value to `obj.property = value`, JavaScript _always_ tries to create or modify `property` directly on `obj`. It does _not_ modify the prototype unless it's an accessor property (getter/setter).
        
- ↪️ Accessor properties are an exception, as assignments are handled by a setter function. So writing to such a property is actually same as calling a function.
    
    ```js
    let user = {
        name: "John",
        surname: "Smith",
    
        set fullName(value) { // This is an accessor property (setter)
            console.log("Setter called!");
            [this.name, this.surname] = value.split(" ");
        },
    
        get fullName() { // This is an accessor property (getter)
            console.log("Getter called!");
            return `${this.name} ${this.surname}`;
        }
    };
    
    let admin = {
        __proto__: user, // user is prototype of admin
        isAdmin: true
    };
    
    console.log(admin.fullName); // Output: Getter called! John Smith (*) getter called
    // Explanation: 'fullName' is not on 'admin', so JS looks up the prototype chain to 'user'.
    // The 'user.fullName' getter is found and executed. Inside the getter, 'this' refers to 'admin' (the object before the dot).
    // So it correctly accesses admin.name (which is inherited from user) and admin.surname (also inherited).
    
    // setter triggers!
    admin.fullName = "Alice Cooper"; // (**) setter called
    // Explanation: 'fullName' is not on 'admin' but its setter is found on 'user' via the prototype chain.
    // The 'user.fullName' setter is executed. Inside the setter, 'this' refers to 'admin'.
    // So, `[this.name, this.surname] = value.split(" ");` creates/updates 'name' and 'surname' properties directly on the 'admin' object.
    
    console.log(admin.fullName); // Output: Getter called! Alice Cooper (***) data of admin modified
    // Explanation: 'fullName' is still not on 'admin', so the getter on 'user' is called.
    // Inside the getter, 'this' refers to 'admin'. Now 'admin' has its own 'name' and 'surname' properties,
    // so it uses those.
    
    console.log(user.fullName); // Output: Getter called! John Smith; (****) user prototype
    // Explanation: 'user.fullName' accesses the getter directly on 'user'.
    // Inside the getter, 'this' refers to 'user', so it uses user.name and user.surname, which were never changed.
    ```
    

### The Value of `this`

this is not effected by prototype at all.

No matter where the method is found: in an object or its prototype. In a method call this always refers to the object before the dot.

- **Explanation:** This is a fundamental rule. When you call a method like `obj.method()`, `this` inside `method` will _always_ be `obj`, regardless of whether `method` was found directly on `obj` or somewhere up its prototype chain.
    

So, setter call at `(**) admin.fullName` uses `admin` as `this`, not `user`.

- **Example (reiterating):**
    
    ```js
    const parent = {
        name: "Parent",
        sayHello() {
            console.log(`Hello from ${this.name}`);
        }
    };
    
    const child = {
        name: "Child",
        __proto__: parent
    };
    
    child.sayHello(); // Output: Hello from Child
    // Explanation: 'sayHello' is found on 'parent', but it's called on 'child'.
    // So, 'this' inside 'sayHello' refers to 'child', and 'this.name' resolves to 'Child'.
    ```
    
- `for...in` loop iterates over inherited properties too.
    
    - **Explanation:** The `for...in` loop is designed to iterate over all _enumerable_ properties of an object, including those inherited from its prototype chain.
        
    - **Example:**
        
        ```js
        const proto = { protoProp: 1 };
        const obj = { ownProp: 2, __proto__: proto };
        
        for (let key in obj) {
            console.log(key);
        }
        // Output:
        // ownProp
        // protoProp
        ```
        
- `obj.hasOwnProperty(key)` -> returns `true` if `key` property is on `obj` (not inherited).
    
    - **Explanation:** This method is crucial for distinguishing between an object's _own_ properties and those it inherits. It returns `true` only if the property is directly defined on the object itself.
        
    - **Example:**
        
        ```js
        const proto = { protoProp: 1 };
        const obj = { ownProp: 2, __proto__: proto };
        
        console.log(obj.hasOwnProperty('ownProp'));   // Output: true
        console.log(obj.hasOwnProperty('protoProp')); // Output: false (inherited)
        console.log(obj.hasOwnProperty('toString'));  // Output: false (inherited from Object.prototype)
        ```
        
- ↪️ Other properties inherited from `Object.prototype` are not enumerable.
    
    - **Explanation:** Methods like `toString`, `valueOf`, `hasOwnProperty`, etc., which are inherited by all objects from `Object.prototype`, have their `enumerable` flag set to `false`. This is why they don't appear when using `for...in` or `Object.keys()`, preventing clutter.
        
    - **Example:**
        
        ```js
        const myObject = {};
        console.log(Object.getOwnPropertyDescriptor(Object.prototype, 'toString'));
        // Output will show 'enumerable: false'
        ```


---
## References