
2025-07-07 14:17

Status:

Tags: [Interview Prep](../3%20-%20Tags/Interview%20Prep.md)

---
# Interview prep 07-07-25

---

## 🟨 JavaScript Fundamentals (10+ Questions)

These test knowledge of the language itself—variables, functions, scoping, hoisting, and more.

1. What is the difference between `var`, `let`, and `const`?
    - `var` is re-declarable and doesn't  respect block scopes.
    - `let` doesn't allow re-declaration and respect block level scopes
    - var and let are mutable
    - variable declared with const is not reassignable.
	-  > Avoid **`var`** in modern JavaScript—it's error-prone due to its function scope and hoisting behavior. 
	- [What is the difference between var, let, and const - JavaScript](Frontend/Javascript%20notes/What%20is%20the%20difference%20between%20var,%20let,%20and%20const%20-%20JavaScript.md)
2. Explain **hoisting**. What gets hoisted in JavaScript?
	- Hoisting is a phenomena where a function or variable declared acts like its declared at top of the scope and can be accessed anywhere.
	- **Hoisting** is JavaScript’s behavior of **moving declarations to the top** of their containing scope (global or function) during the **compilation phase**—before the code is executed.
		- Let and const are hoisted but cannot be used before declaration -  **Temporal Dead Zone** (TDZ)
	- [Hoisting - Javascript](Frontend/Javascript%20notes/Hoisting%20-%20Javascript.md)
    
3. What is a **closure**? Can you give a practical example?
	- A **closure** is formed when an **inner function remembers and continues to access variables** from its **outer function’s scope**, even **after the outer function has returned**. 
	- [ closure - Javascript](%20closure%20-%20Javascript)
    
4. What are **truthy** and **falsy** values in JavaScript?
	- [Truthy and Falsy Values - JavaScript](Frontend/Javascript%20notes/Truthy%20and%20Falsy%20Values%20-%20JavaScript.md)
    - 
5. What is the difference between `==` and `===`?
	- Loose equality vs strict equality
	- [ What is the difference between == and === - Javascript](%20What%20is%20the%20difference%20between%20==%20and%20===%20-%20Javascript)
    
6. What is the difference between **null** and **undefined**?
    - `null` means intentional absence.
    - `Undefined` means unintentional absence.
    - [null vs undefined - Javascript](Frontend/Javascript%20notes/null%20vs%20undefined%20-%20Javascript.md)
7. How does **event delegation** work in JavaScript?
    - **Event Delegation** is a pattern where instead of adding event listeners to many individual child elements, you add **one event listener to a common parent** and **use `event.target` to detect which child triggered the event.**
    - [Event delegation - JavaScript](Frontend/Javascript%20notes/Event%20delegation%20-%20JavaScript.md)
8. What are **arrow functions** and how are they different from regular functions?
   - Arrow function do not bind "this"
   - [Arrow Function and how it is different from others - Javascript](Frontend/Javascript%20notes/Arrow%20Function%20and%20how%20it%20is%20different%20from%20others%20-%20Javascript.md)
    
10. What is a **callback function**? Can you provide an example?
    - > A **callback function** is a **function passed as an argument** to another function — and is **called ("called back") later**, usually after some operation is complete.
    - 
11. What is **the event loop**, and how does JavaScript handle asynchronous operations?
	- The **event loop** is the **mechanism that allows JavaScript to perform non-blocking asynchronous operations**, like timers, DOM events, and HTTP requests — even though it runs on **a single thread**.
    - 
13. What are **template literals** and how do they help?
	- **Template literals** (also called **template strings**) are one of JavaScript's most useful modern features introduced in **ES6** — they make working with strings much easier and more readable.
	- [Template literals - Javascript](Frontend/Javascript%20notes/Template%20literals%20-%20Javascript.md)
14. What does `"use strict"` do in JavaScript?
15. 
    

---

## ⚙️ JavaScript Advanced Concepts (10+ Questions)

These go deeper into asynchronous patterns, OOP, memory management, and best practices.

1. What is the difference between `call()`, `apply()`, and `bind()`?
	- **`this`** context is controlled using `.call()`, `.apply()`, and `.bind()`.

| Method    | What It Does                                                              | When It Runs          |     |
| --------- | ------------------------------------------------------------------------- | --------------------- | --- |
| `call()`  | Calls the function **immediately**, with `this` set to the first argument | Immediately           |     |
| `apply()` | Just like `call()`, but **arguments are passed as an array**              | Immediately           |     |
| `bind()`  | Returns a **new function** with bound `this`, which you can call later    | Later (when you want) |     |
2. What is **currying**, and when would you use it?
	- Currying in JavaScript is a functional programming technique that transforms a function taking multiple arguments into a sequence of functions, each taking a single argument.
    
3. How does JavaScript handle **prototypal inheritance**?
	- In JavaScript, every object has an internal link to another object called its prototype. This link is typically accessed via the `[Prototype](Prototype)` internal property, or historically through the `__proto__` property (though `Object.getPrototypeOf()` and `Object.setPrototypeOf()` are the preferred modern methods
	- This differs from the class-based inheritance found in many other object-oriented languages.
    
4. What is a **Promise**? How is it different from a callback?
	- Promises offer a more structured and cleaner way to handle asynchronous operations compared to callbacks, especially when dealing with multiple dependent operations or error handling
	- Promises are  JavaScript objects representing the eventual completion (or failure) of an asynchronous operation and its resulting value.
    
5. How does `async/await` work under the hood?
	- The `async` keyword, when applied to a function, automatically makes it return a promise. If the `async` function returns a value, that value is wrapped in a resolved promise. If it throws an error, the promise is rejected.
	- The `await` keyword can only be used inside an `async` function. When `await` is used with a promise, it pauses the execution of the `async` function. The execution context of the `async` function is temporarily removed from the call stack, and the event loop is given a chance to execute other tasks.
	- The event loop manages the execution of asynchronous operations. When an `await`ed promise resolves, the continuation of the `async` function (the code following the `await`) is added to the microtask queue. The event loop prioritizes microtasks over other tasks (like callbacks from `setTimeout` or `setInterval`).
    
7. What are **generators** and how are they useful?
    - In JavaScript, generators are special functions capable of pausing their execution and resuming it later. They are defined using the `function*` syntax and employ the `yield` keyword to pause and return a value. When a generator is called, it returns a generator object, which is a type of iterator. This object has a `next()` method that, when called, resumes the generator's execution from where it left off until the next `yield` statement or the end of the function.
8. What is **debouncing** and **throttling**? How do they differ?
    
9. How does **memory leak** happen in JavaScript, and how can you prevent it?
    - A memory leak in JavaScript occurs when objects that are no longer needed by the program are not properly released from memory, preventing the garbage collector from reclaiming that memory. This leads to an accumulation of unused memory, which can degrade performance and potentially crash the application.
10. How do **modules** work in JavaScript (`import`, `export`, `require`)?
    
11. What is the difference between **shallow copy** and **deep copy** in JavaScript?
    

---

## 🧩 JavaScript in the Browser (10+ Questions)

Browser-specific questions that affect DOM manipulation, events, and APIs.

1. What is the DOM and how is it different from the virtual DOM?
	 - The Document Object Model (DOM) is a programming interface for web documents, representing the HTML or XML structure as a tree of objects that can be manipulated by JavaScript. The virtual DOM (VDOM) is a lightweight, in-memory representation of the DOM, used by frameworks like React to optimize updates to the actual DOM. The key difference is that ==the virtual DOM allows for efficient updates by minimizing direct manipulation of the real DOM==
    
2. What is the difference between `e.preventDefault()` and `e.stopPropagation()`?
    -  Prevents the browser's default behavior for the specific event from occurring.
    - Stops the event from propagating further through the DOM hierarchy. Prevents the event from reaching other event listeners on parent or child elements in the DOM tree.
3. What is **localStorage**, **sessionStorage**, and **cookies**? How do they differ?
    
4. How do you manipulate the DOM using plain JavaScript?
	- 
    
5. What is the difference between synchronous and asynchronous execution in the browser?
    - Tasks are executed sequentially, one after another. Each operation must finish before the next one can begin. blocking" model
    - - **Synchronous:** Like doing one task at a time, where you have to finish one before starting the next.
    - Tasks can run independently, without blocking the main thread. This allows other operations to continue while waiting for a task to complete. "non-blocking" model."
    - **Asynchronous:** Like multitasking, where you can start a task and move on to others while waiting for the first one to finish
6. What are **web workers**, and when would you use them?
	-  Web workers are ==a powerful feature in web development that allow you to run JavaScript code in the background, separate from the main thread of your web application==.
	- Web Workers are **a simple means for web content to run scripts in background threads**. The worker thread can perform tasks without interfering with the user interface. In addition, they can make network requests using the fetch() or XMLHttpRequest APIs
    
7. How do you handle errors globally in JavaScript?
	- Global error handling in JavaScript can be implemented using the `window.onerror` event handler for unhandled synchronous errors and the `window.addEventListener('unhandledrejection', ...)` for unhandled Promise rejections.
    
8. What is a **polyfill** and when should you use it?
    
9. What is **CORS**, and how do you handle it in a full stack project?
    - **CORS (Cross-Origin Resource Sharing)** is a browser security feature that regulates requests for resources from a different domain than the one the web page originated from. It extends the **Same-Origin Policy** to allow controlled cross-origin communication. This is particularly relevant in full-stack projects where the front-end and back-end operate on different origins
    - Web browsers enforce the Same-Origin Policy, preventing scripts from accessing resources on a different origin to enhance security. CORS provides a mechanism for servers to specify which origins are allowed to access their resources. When a cross-origin request is made, the browser includes an `Origin` header, and the server responds with CORS headers like `Access-Control-Allow-Origin` to indicate if the request is permitted.
10. How do you handle **lazy loading** in the browser?
    - Lazy loading in browsers is a technique to defer the loading of images and other resources until they are needed, usually when they scroll into the viewport. This improves initial page load times and overall website performance. The primary method is using the `loading="lazy"` attribute on `<img>` and `<iframe>` tags, but other techniques involve JavaScript libraries or frameworks

---

## 🧠 Bonus: Real-World JavaScript Scenarios

1. What happens if you `console.log(this)` inside:
    
    - A regular function
        
    - An arrow function
        
    - A React component
        
2. Why would you use `Object.freeze()` or `Object.seal()`?
    
3. Explain the difference between `Array.prototype.map()` vs `forEach()` vs `reduce()`.
    

---

Would you like a **flashcard version**, **mock answers**, or practice **code snippets** for any of these JavaScript topics?


## 🧠 React Fundamentals (10+ Questions)

1. What is the virtual DOM, and how does React use it?
    - The virtual DOM (VDOM) is ==a lightweight, in-memory representation of the actual Document Object Model (DOM) used by React==. It allows React to optimize UI updates by minimizing direct manipulation of the real DOM, which can be slow and inefficient. React uses the virtual DOM to track changes in the application state and efficiently update only the necessary parts of the real DOM
2. Explain the component lifecycle in class-based components.
    - In React, components have a lifecycle that consists of different phases. Each phase has a set of lifecycle methods that are called at specific points in the component's lifecycle. These methods allow you to control the component's behavior and perform specific actions at different stages of its lifecycle.
    - A component's lifecycle has three main phases: the Mounting Phase, the Updating Phase, and the Unmounting Phase.
    - The Mounting Phase begins when a component is first created and inserted into the DOM. The Updating Phase occurs when a component's state or props change. And the Unmounting Phase occurs when a component is removed from the DOM.
    - The `constructor()` method is called when the component is first created. You use it to initialize the component's state and bind methods to the component's instance. Here's an example:
    - The `render()` method is responsible for generating the component's virtual DOM representation based on its current props and state. It is called every time the component needs to be re-rendered, either because its props or state have changed, or because a parent component has been re-rendered.
    - During the mounting phase, `getDerivedStateFromProps()` is called after the constructor and before `render()`. This method is called for every render cycle and provides an opportunity to update the component's state based on changes in props before the initial render.
    - The `componentDidMount()` method is called once the component has been mounted into the DOM. It is typically used to set up any necessary event listeners or timers, perform any necessary API calls or data fetching, and perform other initialization tasks that require access to the browser's DOM API.
    - The `shouldComponentUpdate()` method is called before a component is updated. It takes two arguments: `nextProps` and `nextState`. This method returns a boolean value that determines whether the component should update or not. If this method returns true, the component will update, and if it returns false, the component will not update.
    - `componentWillUpdate()` is a lifecycle method in React that gets called just before a component's update cycle starts. It receives the next prop and state as arguments and allows you to perform any necessary actions before the component updates.
    - The `componentDidUpdate()` method is a lifecycle method in React that is called after a component has been updated and re-rendered. It is useful for performing side effects or additional operations when the component's props or state have changed.
    - - `componentWillUnmount()`: This method is called just before the component is removed from the DOM. It allows you to perform any necessary cleanup, such as canceling timers, removing event listeners, or clearing any data structures that were set up during the mounting phase.
3. What are functional components, and how are they different from class components?
    - A ****functional component**** is a simpler way to define components in React using JavaScript functions. Unlike class components, functional components do not require a constructor or lifecycle methods. They are typically used for components that are presentational and do not manage complex state or lifecycle events.
    - A class component is one of the two ways to define components in React, the other being functional components. Class components are ES6 classes that extend React.Component and can hold and manage internal state.
4. What are keys in React, and why are they important?
    - In React, "keys" are special string attributes that must be included when creating lists of elements, typically when mapping over an array to render multiple components. Keys serve as a hint to React's reconciliation algorithm, helping it efficiently identify which items in a list have changed, are added, or are removed.
5. How does React handle re-renders? What causes unnecessary re-renders?
    - - When a component's internal state (managed by `useState` or `this.state`) or its received props change, React schedules a re-render.
6. What are fragments in React? Why might you use them?
    
7. How does `React.memo()` work, and when should you use it?
    - `React.memo()` is a Higher Order Component (HOC) that optimizes the performance of functional components by preventing unnecessary re-renders. When a component is wrapped with `React.memo()`, React will memoize its rendered output and skip re-rendering the component if its props have not changed since the last render.
    - - `React.memo()` performs a shallow comparison of the component's current props with its previous props. This means it checks if the references of the props are the same, not if their values are deeply equal.
    - If the shallow comparison reveals no changes in the props, `React.memo()` prevents the component from re-rendering and instead reuses the previously rendered output.
    - - You can provide a custom comparison function as the second argument to `React.memo()` if the default shallow comparison is not sufficient for your needs (e.g., when dealing with deeply nested objects or arrays as props).
8. What are higher-order components (HOCs)?
    - Higher-Order Components (HOCs) in React are a pattern for reusing component logic. They are functions that take a component as an argument and return a new, enhanced component with additional props or functionality
9. What is prop drilling, and how can it be avoided?
    - Prop drilling in React refers to ==the process of passing data through multiple levels of nested components, even if some of those components don't need the data themselves, simply to get it to a deeply nested component==. This can lead to less maintainable and harder-to-refactor code, especially as the component hierarchy grows
    - React context, Redux
10. Explain reconciliation in React.
    - Reconciliation in React is the process by which React efficiently updates the User Interface (UI) in response to changes in a component's state or props. It is a core mechanism that underpins React's performance optimizations and its declarative programming model.
11. What’s the difference between controlled and uncontrolled components?
    - In React, the key difference between controlled and uncontrolled components lies in how they manage form input values. ==Controlled components have their input values managed by React's state, meaning React controls the value and any changes trigger a re-render.== ==Uncontrolled components rely on the DOM (Document Object Model) to manage their values==, similar to traditional HTML forms, and their values are accessed via refs
12. How does React update the UI efficiently when the state changes?
    - 

---

## ⚙️ React Hooks & State Management (10+ Questions)

1. What is the purpose of the `useEffect` hook? How does the dependency array affect its behavior?
    - The `useEffect` hook in React is designed ==to handle side effects within functional components==. These side effects can include actions like fetching data, directly manipulating the DOM, or setting up subscriptions. The hook allows you to perform these actions after the component renders, ensuring that the UI is fully updated before any side effects are applied
    - The dependency array, passed as the second argument to `useEffect`, plays a crucial role in controlling when the effect function is executed. 

2. What is the difference between `useState` and `useReducer`?
    - `useState` and `useReducer` are both React hooks used for managing state in functional components, but they differ in complexity and scope. `useState` is suitable for simple, independent state updates, while `useReducer` is designed for more complex state logic involving multiple related values or when the next state depends on the previous one
3. How does `useCallback` help with performance?
    - `useCallback` is ==a React Hook that memorizes functions, ensuring they maintain a stable reference across renders unless their dependencies change==. This helps optimize performance by preventing unnecessary re-renders in child components, especially when passing functions as props.
    - When a parent component re-renders, it can cause its child components to also re-render, even if the child component's props haven't changed. If a child component receives a function as a prop and that function is recreated on every render, the child component will unnecessarily re-render. By using `useCallback` to memoize the function, you ensure that the child component only re-renders when the function's dependencies change, preventing wasted re-renders.
4. What is `useRef`, and when would you use it?
    - `useRef` is ==a React Hook that provides a way to persist values between renders without causing a re-render==.
    - commonly used to: access and manipulate DOM elements directly, store mutable values that don't trigger re-renders, and hold references to values that need to persist across renders
5. When does `useMemo` help optimize performance?
    - `useMemo` in React helps optimize performance by **memoizing the result of a function**, meaning it caches the output of a function and only re-computes it when its dependencies change. This prevents unnecessary calculations on re-renders, making your application feel faster, especially when dealing with complex or expensive operation
6. Can you create custom hooks? Give an example.
    - Custom hooks are simply JavaScript functions that begin with the prefix "use" and allow you to extract and reuse logic from components. They enable you to leverage other built-in React hooks like `useState`, `useEffect`, and `useContext` within your custom hooks, promoting code organization and reusability
7. How would you implement global state without Redux?
    - To implement global state management in a React application without Redux, you can leverage the React Context API and the `useReducer` hook. This approach allows you to share state across multiple components without prop drilling and provides a more streamlined way to manage complex state logic.
8. What are some differences between Redux and Zustand?
    - 
9. How do you persist state across sessions?
    - 
10. What’s the difference between Context API and Redux?
    - Context API is a built-in React feature for sharing data across the component tree, while Redux is a separate library with a more robust, centralized state management system
11. What’s a good pattern to manage forms in React?
    

---

## ⚛️ Next.js Specifics (10+ Questions)

1. What’s the difference between SSR, SSG, and ISR in Next.js?
    - SSR (Server-Side Rendering) generates HTML on each request, SSG (Static Site Generation) pre-renders pages at build time, and ISR (Incremental Static Regeneration) combines SSG with the ability to update static pages periodically
2. When should you use `getServerSideProps` vs `getStaticProps`?
    - `getStaticProps` - Data is fetched during the build process, and a static HTML page is generated.
    - `getServerSideProps` - Data is fetched on _each_ request to the server, and the page is rendered dynamically.
3. How does routing work in Next.js? What is file-based routing?
    - In Next.js, routing is a fundamental aspect that determines how your application navigates between different pages and resources. It's built on a **file-system based routing** system, which simplifies route management and offers a more intuitive approach compared to traditional methods that rely on centralized configuration files
4. What are dynamic routes, and how are they implemented in Next.js?
    
5. How do API routes work in Next.js?
    
6. What are middleware functions in Next.js 13+?
    
7. How do you handle environment variables in a Next.js project?
    
8. What is the difference between the pages and app directory in Next.js 13+?
    
9. How would you secure an API route in Next.js?
    
10. What are Layouts in Next.js, and how do they help with UI reuse?
    
11. How would you optimize images using Next.js?
    

---

## 🎨 UI/UX and Performance Optimization (10+ Questions)

1. How do you implement code-splitting in React or Next.js?
    - Code splitting in React and Next.js involves breaking down your application's JavaScript bundle into smaller, more manageable chunks that can be loaded on demand. This improves performance by reducing the initial load time.
2. What are some strategies for lazy-loading components?
    - `React.lazy()` and `Suspense`: This is the primary method for component-level code splitting.
		- `React.lazy()` allows you to render a dynamic import as a regular component. It takes a function that returns a Promise, which resolves to a module containing a React component.
		- `Suspense` is used in conjunction with `React.lazy()` to display a fallback UI (like a loading indicator) while the lazy-loaded component is being fetched and rendered
3. How do you use the `next/image` component, and what are its benefits?
    
4. What tools do you use to measure frontend performance?
    - Frontend performance is typically measured using a combination of tools, including ==browser developer tools, dedicated performance monitoring platforms, and real-user monitoring==
5. How do you minimize bundle size in a React or Next.js app?
    - Minimizing bundle size in a React or Next.js application is crucial for improving loading times and overall performance. Several strategies can be employed to achieve this:
6. How do you handle font loading optimization in Next.js?
    - 
7. How would you improve perceived performance?
    
8. What is the role of web vitals in Next.js, and how do you track them?
    
9. How would you reduce re-rendering in a React component?
    
10. What accessibility best practices do you follow in React?
    
11. How do you handle responsiveness in your apps?
    

---

## 🐍 Django Fundamentals & ORM (10+ Questions)

1. What are models in Django, and how do you define them?
    
2. Explain how Django ORM works.
    
3. How does Django handle database migrations?
    
4. What is the difference between `OneToOneField`, `ForeignKey`, and `ManyToManyField`?
    
5. How do you write raw SQL queries in Django if needed?
    
6. What’s the difference between `select_related` and `prefetch_related`?
    
7. What is the use of `Meta` class inside a model?
    
8. How would you create custom model managers?
    
9. How do you validate data at the model level?
    
10. How would you handle bulk insert or update in Django ORM?
    
11. How would you log SQL queries for debugging?
    

---

## 🔌 Django Views, API & Serialization (10+ Questions)

1. What are function-based views (FBV) and class-based views (CBV)? Which do you prefer and why?
    
2. What is Django REST Framework (DRF), and how does it work?
    
3. How do serializers work in DRF?
    
4. What is the difference between `ModelSerializer` and a regular `Serializer`?
    
5. How do you create a custom viewset?
    
6. How would you implement pagination in an API?
    
7. How do you apply filtering and search on a queryset via DRF?
    
8. What are throttling and rate-limiting? How do you implement them?
    
9. How do you handle authentication and permissions in DRF?
    
10. How do you secure an API endpoint in Django?
    
11. How would you test a Django API?
    

---

## 🧱 Django Admin, Forms & Templates (10+ Questions)

1. How do you customize the Django admin panel?
    
2. How do you add filters, search fields, and custom list displays in admin?
    
3. What are the differences between ModelForms and regular Forms?
    
4. How do you perform custom validation in a form?
    
5. How do you render form fields manually in a template?
    
6. What are template filters and template tags?
    
7. How would you prevent form resubmission on refresh?
    
8. How do CSRF tokens work in Django forms?
    
9. How do you handle file uploads via forms?
    
10. How would you handle dynamic form fields?
    
11. How do you organize reusable templates?
    

---

## 🧠 System Design / Full Stack Integration (10+ Questions)

1. How do you structure a full-stack React + Django project?
    
2. How would you handle login/signup with JWT in a full-stack setup?
    
3. How do you deploy React and Django together on platforms like Heroku or Vercel + Render?
    
4. How would you ensure secure communication between frontend and backend?
    
5. How would you implement file uploads from React to Django backend?
    
6. What’s your preferred way to manage environment configs across frontend/backend?
    
7. How would you handle rate limiting on your backend?
    
8. How would you secure sensitive API keys in production?
    
9. How do you handle long-running tasks in Django (e.g., Celery)?
    
10. How do you implement real-time notifications in a full-stack app?
    
11. How would you scale your backend if your app becomes very popular?
    

---

## 🗄️ Database Fundamentals (10+ Questions)

These assess your understanding of relational and NoSQL concepts, SQL queries, optimization, and how they apply in Django projects.

1. What’s the difference between SQL and NoSQL databases? When would you use each?
    
2. Explain normalization. What are 1NF, 2NF, and 3NF?
    
3. What are indexes? How do they improve performance, and when can they hurt it?
    
4. What’s the difference between an inner join, left join, and right join?
    
5. How does Django ORM handle joins under the hood?
    
6. What’s a transaction in a database? How do you manage it in Django?
    
7. How do you prevent SQL injection?
    
8. What are primary keys vs foreign keys?
    
9. How would you model a one-to-many and many-to-many relationship in SQL and in Django?
    
10. How do ACID properties help ensure data integrity?
    
11. What is denormalization and when is it beneficial?
    
12. How do you track schema changes and version control your database?
    
13. How would you index a JSON field in PostgreSQL or handle semi-structured data?
    

---

## 📡 API Design & Integration (10+ Questions)

These questions test your understanding of RESTful principles, authentication, error handling, and integration from frontend to backend.

1. What are the key principles of REST architecture?
    
2. How would you design a RESTful API for a blog (e.g., CRUD for posts and comments)?
    
3. What are HTTP status codes? Name a few commonly used ones and what they mean.
    
4. What’s the difference between PUT and PATCH?
    
5. How do you handle authentication for APIs (e.g., JWT, Session Auth)?
    
6. How do you secure sensitive endpoints from unauthorized access?
    
7. How do you handle API rate limiting and throttling?
    
8. How do you manage error handling in both frontend and backend when consuming APIs?
    
9. What tools have you used to test APIs (e.g., Postman, Swagger, curl)?
    
10. How do you deal with CORS issues when React accesses a Django backend?
    
11. What are idempotent methods? Why is it important for APIs?
    
12. How would you version your APIs for long-term support?
    
13. What’s the difference between REST and GraphQL?
    

---

### 💡 Bonus: Cross-topic Questions

To test how well candidates integrate database + API + frontend:

- If a user updates their profile photo from the React frontend, walk me through what happens across the stack until it’s saved and displayed.
    
- How would you debug a situation where a React form submits data but nothing changes in the Django database?
    
- Suppose an API is slow — how would you identify if it's a backend DB issue or a frontend request issue?

### **Section 1: Behavioral & Motivational Questions**

These questions assess your personality, motivation, and fit with the organization's collaborative, mission-driven culture.

**1. Tell me about yourself. / Walk me through your resume.**

- **Your Answer:** "I'm a software developer with over three years of full-stack experience, primarily focused on building user-centric applications with React, Next.js, and Python. At Target, I contributed to the full development lifecycle, starting with UI development for internal merchandising dashboards and progressively taking on more backend responsibilities. I'm particularly proud of leading an initiative to build a reusable component library that reduced front-end development effort by 25% and optimizing dashboard performance, which improved load times by 30%. I recently completed my Master's in Information Systems with a focus on Information Assurance, which has given me a strong security-first mindset. I'm really passionate about using my skills for social impact, which is why I was so drawn to Digital Aid Seattle's mission. I'm eager to apply my front-end expertise to help bridge the digital divide."
    

**2. Why are you specifically interested in volunteering for Digital Aid Seattle?**

- **Your Answer:** "I've been following Digital Aid Seattle's work and I'm deeply impressed by your mission to provide technology access and skills to underserved communities. It's not just about giving people devices; it's about empowering them. My experience building intuitive and efficient user interfaces, like the analytics dashboards at Target, directly translates to your goal of creating accessible technology. I want to contribute my skills in React and my focus on performance and usability to a cause that has a tangible, positive impact on people's lives, and I believe your organization is the perfect place to do that."
    

**3. What are your greatest strengths as a developer?**

- **Your Answer:** "I'd say my greatest strengths are my proficiency in the modern React ecosystem, my focus on performance, and my collaborative nature. My experience with React, Next.js, and Tailwind CSS allows me to build modern, responsive UIs efficiently. As for performance, at Target, I successfully reduced API response times by 35% and front-end load times by 30%, showing I can analyze and solve bottlenecks across the stack. Finally, I thrive in collaborative Agile environments; I enjoy working with cross-functional teams, defining requirements, and mentoring junior developers, which I believe would be a great asset in a volunteer team setting."
    

**4. What is a weakness you're working on?**

- **Your Answer:** "In the past, I sometimes got too focused on the technical details of a feature and might have missed the broader business context. I've been actively working on this by making a conscious effort to ask more 'why' questions during sprint planning and engaging more with product owners and users. For instance, in my last role, I started setting up brief, informal check-ins with business users of the dashboards I was building. This helped me better understand their needs and ultimately build more impactful tools."
    

**5. Describe a time you faced a major technical challenge and how you overcame it.**

- **Your Answer:** "**(S)ituation:** We had a critical internal dashboard at Target that was becoming unusably slow as the data grew. **(T)ask:** My task was to diagnose and fix the performance issues. **(A)ction:** I used Chrome DevTools to profile the front-end and found that large, unoptimized component re-renders were the main culprit. I implemented `React.memo` and `useCallback` to prevent unnecessary re-renders. I also collaborated with the backend team to introduce pagination to the API and optimized some PostgreSQL queries with better indexing. **(R)esult:** These changes led to a 30% improvement in load times and a much smoother user experience, which was a significant win for the merchandising team."
    

**6. How do you handle disagreements within a team?**

- **Your Answer:** "I believe the best approach is open and respectful communication. I focus on understanding the other person's perspective by listening carefully to their reasoning. I then try to find common ground by focusing on our shared goal, which is to build the best possible product. I would present my own view with data or evidence if possible, and be open to a compromise that serves the project's best interests. It's about finding the right solution, not about being right."
    

### **Section 2: JavaScript Core Concepts**

**1. What is the difference between `var`, `let`, and `const`?**

- **Your Answer:** "`var` is function-scoped and can be re-declared and updated. `let` and `const` are block-scoped, introduced in ES6. `let` allows a variable to be updated but not re-declared within the same scope. `const` declares a variable that cannot be reassigned. I use `const` by default for all variables to prevent accidental reassignment and switch to `let` only when I know the value needs to change."
    

**2. Explain hoisting in JavaScript.**

- **Your Answer:** "Hoisting is JavaScript's behavior where it moves declarations of functions and variables to the top of their containing scope during the compilation phase. This means you can call a function before you've written it in the code. However, for variables declared with `var`, only the declaration is hoisted, not the initialization, so it will be `undefined` until assigned. For `let` and `const`, they are hoisted but enter a 'temporal dead zone,' meaning you can't access them before the line of declaration, which helps prevent bugs."
    

**3. What is a closure? Can you give a practical example?**

- **Your Answer:** "A closure is a function that remembers and has access to variables from its outer (enclosing) scope, even after that outer function has returned. A classic example is a counter function. The outer function might have a `count` variable and return an inner function. Each time you call the inner function, it can increment and return the `count`, but the `count` variable itself is not accessible from the global scope, effectively making it private."
    

**4. What is the difference between `==` and `===`?**

- **Your Answer:** "`==` is the loose equality operator. It performs type coercion, meaning it tries to convert the operands to the same type before comparison. For example, `5 == '5'` is true. `===` is the strict equality operator. It does not perform type coercion; it checks for both value and type equality. `5 === '5'` is false. I exclusively use `===` in my code to avoid unexpected bugs from type coercion."
    

**5. Explain the event loop and how JavaScript handles asynchronous operations.**

- **Your Answer:** "Even though JavaScript is single-threaded, it handles asynchronous operations without blocking the main thread using the event loop. When an async operation like a `fetch` request or `setTimeout` is called, it's handed off to the browser's Web API. Once the operation is complete, its callback function is placed in the callback queue. The event loop constantly checks if the call stack is empty. If it is, it takes the first event from the queue and pushes it onto the call stack to be executed. This mechanism allows the UI to remain responsive."
    

**6. What are `call()`, `apply()`, and `bind()`?**

- **Your Answer:** "All three are methods used to set the `this` context for a function. `call()` and `apply()` invoke the function immediately. The difference is how they take arguments: `call()` takes a list of arguments, while `apply()` takes an array of arguments. `bind()`, on the other hand, does not call the function immediately. It returns a new function with the `this` context and any initial arguments 'bound' to it, which can be called later. I've used `bind()` in older class components to bind event handlers to the component instance."
    

**7. What is prototypal inheritance?**

- **Your Answer:** "Prototypal inheritance is JavaScript's native inheritance model. Instead of classes inheriting from other classes, objects inherit directly from other objects. Every object has an internal link to another object called its 'prototype'. When you try to access a property on an object, if it's not on the object itself, the JavaScript engine looks up the prototype chain until it finds the property or reaches the end of the chain (`null`)."
    

**8. What is the difference between a shallow copy and a deep copy?**

- **Your Answer:** "A shallow copy of an object or array creates a new object/array, but it only copies the references to any nested objects or arrays. So, if you change a nested object in the copy, it also changes in the original. A deep copy, conversely, creates a new object/array and recursively copies all nested objects and arrays, so the copy is completely independent of the original. I use the spread syntax (`...`) or `Object.assign` for shallow copies, and for deep copies, a common method is `JSON.parse(JSON.stringify(object))`, though I'm aware of its limitations with certain data types."
    

### **Section 3: React & Next.js**

**1. What is the Virtual DOM and how does it improve performance?**

- **Your Answer:** "The Virtual DOM is a lightweight, in-memory representation of the actual DOM. When a component's state changes, React creates a new virtual DOM tree. It then compares this new tree with the previous one in a process called 'reconciliation' or 'diffing'. It calculates the most efficient way to make these changes to the real DOM and then applies only those minimal updates. This avoids costly direct manipulations of the entire DOM tree, which is a major reason for React's high performance."
    

**2. Explain `useState`, `useEffect`, `useCallback`, `useMemo`, and `useRef`.**

- **Your Answer:**
    
    - **`useState`**: Adds state to functional components. It's the hook I use most for managing local component state like form inputs or UI toggles.
        
    - **`useEffect`**: Handles side effects like API calls, subscriptions, or manual DOM manipulations. I use its dependency array to control when the effect runs, for instance, an empty array `[]` for one-time data fetching on mount.
        
    - **`useCallback`**: Memoizes a callback function, preventing it from being recreated on every render. I use this to optimize performance when passing callbacks to child components that are wrapped in `React.memo`, preventing unnecessary re-renders.
        
    - **`useMemo`**: Memoizes the result of a complex calculation. It re-runs the calculation only when one of its dependencies changes. This is useful for optimizing performance by avoiding expensive computations on every render.
        
    - **`useRef`**: Provides a way to access DOM nodes directly or to hold a mutable value that doesn't cause a re-render when it changes. I've used it to manage focus on an input element, for example.
        

**3. What is prop drilling and how do you avoid it?**

- **Your Answer:** "Prop drilling is the process of passing props down through multiple layers of nested components, even if the intermediate components don't need the props themselves. To avoid this, I use the React Context API for sharing global data like theme information or user authentication status. For more complex, application-wide state, I have experience using Redux Toolkit, which provides a centralized store and is more scalable."
    

**4. What is the difference between a controlled and an uncontrolled component?**

- **Your Answer:** "The difference lies in who manages the state of a form element. In a **controlled component**, the form data is handled by React state. The value of the input is driven by a prop, and changes are handled by a callback function like `onChange`. This gives React full control. In an **uncontrolled component**, the form data is handled by the DOM itself. You typically use a `ref` to get the value from the DOM when you need it. I prefer controlled components because they make the state explicit and easier to manage and validate."
    

**5. What is the difference between SSR, SSG, and ISR in Next.js?**

- **Your Answer:**
    
    - **SSR (Server-Side Rendering)** generates the HTML for a page on the server for every request. It's ideal for pages with highly dynamic, user-specific content.
        
    - **SSG (Static Site Generation)** generates the HTML at build time. It's extremely fast because pages can be served from a CDN. This is best for content that doesn't change often, like a blog or marketing pages.
        
    - **ISR (Incremental Static Regeneration)** is a hybrid approach. It allows you to update static pages after they've been built. You can set a revalidation period, and if a request comes in after that period, Next.js will regenerate the page in the background. This gives you the speed of static with the ability to have fresh data."
        

**6. How do you handle code-splitting in a React/Next.js app?**

- **Your Answer:** "In my projects, I've used `React.lazy()` and `Suspense` to implement code-splitting at the component level. This allows me to load components only when they are needed. Next.js makes this even easier with its file-system-based routing, as it automatically code-splits by page. This is a key practice I used at Target to reduce initial bundle sizes and improve load times, as noted on my resume."
    

### **Section 4: Django & Backend Integration**

**1. Explain how the Django ORM works.**

- **Your Answer:** "The Django ORM (Object-Relational Mapper) is a powerful feature that lets me interact with the database using Python code instead of writing raw SQL. I define my database schema in Python by creating model classes. Each class maps to a database table, and each attribute on the class maps to a table column. The ORM then translates my Python queries, like `Post.objects.filter(author='Ganesh')`, into efficient SQL queries, handles the database connection, and returns the results as Python objects. It abstracts away the database-specific SQL, making the code more portable and secure."
    

**2. What’s the difference between `select_related` and `prefetch_related`?**

- **Your Answer:** "Both are performance optimization tools to reduce database queries. `select_related` works for foreign key and one-to-one relationships. It performs a SQL `JOIN` in a single query, retrieving the related objects along with the main object. `prefetch_related`, on the other hand, works for many-to-many and many-to-one relationships. It performs a separate lookup for the related objects and then 'joins' them in Python. I would use `select_related` for a blog post and its author (a `ForeignKey`), and `prefetch_related` for a blog post and its tags (a `ManyToManyField`)."
    

**3. What are function-based views (FBV) and class-based views (CBV)? Which do you prefer?**

- **Your Answer:** "Function-based views are simple Python functions that take a request and return a response. They are straightforward and easy to understand. Class-based views use Python classes to handle requests. They offer more structure and reusability through inheritance and mixins. For simple views, an FBV is often quicker. However, for more complex logic that can be reused, like the CRUD operations in my 'Retail Analytics Dashboard' backend, I prefer CBVs, especially the generic views provided by Django REST Framework, as they reduce boilerplate code."
    

**4. How do serializers work in Django REST Framework (DRF)?**

- **Your Answer:** "Serializers in DRF are crucial for building APIs. They have two main jobs: they serialize querysets and model instances into native Python datatypes that can then be easily rendered into JSON or XML. They also deserialize incoming data, validating it first, and then converting it back into complex types like model instances. In my projects, I've heavily used `ModelSerializer`, which automatically generates fields and validators based on a Django model, significantly speeding up API development."
    

### **Section 5: System Design & Full-Stack**

**1. How do you structure a full-stack React + Django project?**

- **Your Answer:** "I typically use a monorepo structure where both the front-end and back-end code live in the same repository but in separate directories, for example, a `frontend` directory for the React app and a `backend` directory for the Django project. This makes it easier to manage. The React app is responsible for the UI and makes API calls to the Django backend, which handles business logic and database interactions. For deployment, they are often run as separate services, with a web server like Nginx routing requests to either the React app or the Django API based on the URL."
    

**2. How would you handle login/signup with JWT in a full-stack setup?**

- **Your Answer:** "The user would submit their credentials from the React front-end to a Django API endpoint. The Django backend would validate the credentials. On success, it would generate two JSON Web Tokens (JWTs): an access token (short-lived) and a refresh token (long-lived). Both tokens are sent back to the React app. The access token is stored in memory and sent in the Authorization header of every subsequent API request. The refresh token is stored securely in an HttpOnly cookie. When the access token expires, the front-end uses the refresh token to silently request a new access token without requiring the user to log in again."
    

**3. How do you deal with CORS issues when React accesses a Django backend?**

- **Your Answer:** "CORS (Cross-Origin Resource Sharing) is a browser security feature. Since my React app (e.g., on `localhost:3000`) and Django API (e.g., on `localhost:8000`) are on different origins, I need to configure the backend to allow requests from the front-end. I use the `django-cors-headers` package. In my Django settings, I configure a whitelist of allowed origins, like `CORS_ALLOWED_ORIGINS = ['http://localhost:3000']`. This tells the browser that it's safe for my React app to make requests to my Django API."
    

**4. Suppose an API is slow. How would you identify if it's a backend DB issue or a front-end request issue?**

- **Your Answer:** "I'd start by using the browser's Network tab in DevTools. I would check the timing breakdown for the slow request. If the 'Waiting (TTFB)' time is high, it strongly suggests a backend problem. To confirm, I'd use a tool like Postman to make the same request directly to the API, bypassing the front-end entirely. If it's still slow, the issue is on the backend. I would then use a tool like the Django Debug Toolbar to inspect the SQL queries being generated. Often, the culprit is an unoptimized query that can be fixed with `select_related`, `prefetch_related`, or better database indexing, which are techniques I've used at Target."
    

### **Section 6: Questions for Them**

Asking thoughtful questions shows your engagement and interest.

1. "Can you describe the team structure for this project? Who would I be collaborating with?"
    
2. "What does the typical development workflow look like here? Do you use Agile, sprints, and code reviews?"
    
3. "What is the biggest technical challenge the team is currently facing that I might be able to help with?"
    
4. "How do you measure the impact of the software you build for the community?"
    
5. "What are the next steps in the interview process?"

### **Section 7: API Design & Integration**

**1. What are the key principles of REST architecture?**

- **Your Answer:** "REST (Representational State Transfer) is an architectural style for designing networked applications. The key principles I follow are:
    
    - **Client-Server Separation:** The client (front-end) and server (back-end) are separate concerns. This allows them to be developed and scaled independently.
        
    - **Statelessness:** Each request from a client to the server must contain all the information needed to understand and complete the request. The server does not store any client context between requests.
        
    - **Cacheability:** Responses must define themselves as cacheable or not. This helps improve performance and scalability.
        
    - **Layered System:** A client cannot ordinarily tell whether it is connected directly to the end server or to an intermediary along the way. This allows for load balancers and proxies.
        
    - **Uniform Interface:** This is the core of REST. It simplifies the architecture and includes using standard HTTP methods (GET, POST, PUT, DELETE), resource-based URIs (like `/posts/123`), and using JSON for resource representation."
        

**2. How would you design a RESTful API for a blog (e.g., CRUD for posts and comments)?**

- **Your Answer:** "I would design the API around resources: `posts` and `comments`.
    
    - **Posts:**
        
        - `GET /api/posts/`: List all posts.
            
        - `POST /api/posts/`: Create a new post.
            
        - `GET /api/posts/{post_id}/`: Retrieve a single post.
            
        - `PUT /api/posts/{post_id}/`: Update a post completely.
            
        - `DELETE /api/posts/{post_id}/`: Delete a post.
            
    - **Comments (as a nested resource of posts):**
        
        - `GET /api/posts/{post_id}/comments/`: List all comments for a specific post.
            
        - `POST /api/posts/{post_id}/comments/`: Create a new comment for a specific post.
            
    - This structure is logical, predictable, and follows RESTful conventions."
        

**3. What are HTTP status codes? Name a few commonly used ones and what they mean.**

- **Your Answer:** "HTTP status codes are standard responses from the server indicating the outcome of a request. I use them constantly.
    
    - **2xx (Success):**
        
        - `200 OK`: The request was successful.
            
        - `201 Created`: The request was successful, and a new resource was created (used with POST).
            
        - `204 No Content`: The request was successful, but there is no content to return (used with DELETE).
            
    - **4xx (Client Errors):**
        
        - `400 Bad Request`: The server could not understand the request due to invalid syntax.
            
        - `401 Unauthorized`: The client must authenticate itself to get the requested response.
            
        - `403 Forbidden`: The client does not have access rights to the content.
            
        - `404 Not Found`: The server cannot find the requested resource.
            
    - **5xx (Server Errors):**
        
        - `500 Internal Server Error`: A generic error message, given when an unexpected condition was encountered."
            

**4. What’s the difference between PUT and PATCH?**

- **Your Answer:** "Both `PUT` and `PATCH` are used for updating resources. The key difference is that `PUT` is for a full update, while `PATCH` is for a partial update. With `PUT`, you must send the entire resource representation. If you omit fields, they might be set to null or a default value. With `PATCH`, you only send the specific fields you want to change, and the rest are left untouched. `PUT` is idempotent, while `PATCH` can be, but isn't necessarily."
    

**5. How do you handle authentication for APIs (e.g., JWT, Session Auth)?**

- **Your Answer:** "As my resume mentions, I have experience with both. In traditional Django apps, session authentication is common and works well. But for decoupled front-ends like a React app, I prefer using JSON Web Tokens (JWT). The flow involves the client sending credentials, the server validating them and returning an access token and a refresh token. The access token is sent with every subsequent request in the `Authorization` header. This approach is stateless, which aligns perfectly with REST principles and scales well."
    

**6. How do you secure sensitive endpoints from unauthorized access?**

- **Your Answer:** "In Django REST Framework, I use a combination of authentication and permission classes. First, I ensure the endpoint requires authentication, for example, by setting a default authentication class like `JWTAuthentication`. Then, I apply permission classes to control access. For instance, `IsAuthenticated` ensures only logged-in users can access the endpoint. For more granular control, I use classes like `IsAdminUser` or create custom permission classes, for example, to ensure only the author of a post can edit or delete it."
    

**7. How do you handle API rate limiting and throttling?**

- **Your Answer:** "Throttling is essential to prevent abuse and ensure fair usage of the API. In Django REST Framework, I can configure throttling policies globally or on a per-view basis. I can set different rates for anonymous users versus authenticated users. For example, I might use `AnonRateThrottle` to limit unauthenticated requests to 100 per day, and `UserRateThrottle` to allow authenticated users 1000 requests per day. This is a crucial part of building robust and reliable APIs."
    

**8. How do you manage error handling in both frontend and backend when consuming APIs?**

- **Your Answer:** "On the **backend** (Django), I use `try...except` blocks for specific errors and let DRF handle standard HTTP errors by returning appropriate status codes and a JSON error message. On the **frontend** (React), when I make an API call using `fetch` or Axios, I use `async/await` within a `try...catch` block. The `try` block handles the 'happy path' and processes the successful response. The `catch` block handles any network or server errors. I check the response status code to differentiate between, say, a 404 (Not Found) and a 500 (Internal Server Error) and update the UI state to show a user-friendly error message accordingly."
    

**9. What tools have you used to test APIs (e.g., Postman, Swagger, curl)?**

- **Your Answer:** "My resume lists Postman and PyTest. I use **Postman** extensively during development for manual testing of my API endpoints. It's great for sending different types of requests, setting headers, and inspecting responses. For automated testing, I use **PyTest** with Django REST Framework's `APIClient` to write unit and integration tests for my API views. This ensures that my API behaves as expected and helps prevent regressions."
    

**10. How do you deal with CORS issues when React accesses a Django backend?**

- **Your Answer:** "I've handled this in all my full-stack projects. CORS (Cross-Origin Resource Sharing) is a browser security mechanism that blocks requests between different origins by default. To solve this, I use the `django-cors-headers` package in my Django backend. I configure it in `settings.py` by adding it to `INSTALLED_APPS` and `MIDDLEWARE`, and then specifying the allowed front-end origins (like `http://localhost:3000` for development) in the `CORS_ALLOWED_ORIGINS` list. This tells the browser that my backend explicitly permits requests from my React application."
    

**11. What are idempotent methods? Why is it important for APIs?**

- **Your Answer:** "An idempotent method is an operation that can be applied multiple times without changing the result beyond the initial application. In HTTP, `GET`, `PUT`, and `DELETE` are idempotent. For example, calling `DELETE /posts/123` five times has the same effect as calling it once. This is important for API reliability. If a client sends a request and gets a network error, it doesn't know if the request was processed. With an idempotent method, the client can safely send the same request again without worrying about creating duplicate resources or other unintended side effects."
    

**12. How would you version your APIs for long-term support?**

- **Your Answer:** "Versioning is critical for evolving an API without breaking existing client applications. The most common method I would use is URI versioning, where the version number is included in the URL, like `/api/v1/posts/`. This is clear and easy to implement. In Django REST Framework, I can use namespaces in my `urls.py` to manage different versions. This allows me to have `v1` and `v2` of an endpoint running simultaneously while I phase out the older version."
    

**13. What’s the difference between REST and GraphQL?**

- **Your Answer:** "REST is an architectural style based on resources and standard HTTP methods. With REST, you typically have multiple endpoints for different resources, and the server determines the structure of the response. The main issues can be over-fetching (getting more data than you need) or under-fetching (having to make multiple requests to get all the data you need). **GraphQL** is a query language for APIs. It uses a single endpoint. The client specifies exactly what data it needs in a query, and the server returns a JSON object with precisely that data, solving the over-fetching and under-fetching problems. While most of my experience is with REST, I am actively learning GraphQL because of its efficiency."
    

---

Would you like me to convert these into a printable **interview packet**, or generate **sample answers** or **live coding challenges** tied to these themes?

---
## References