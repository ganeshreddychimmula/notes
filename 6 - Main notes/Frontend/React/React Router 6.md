
2025-08-21 19:58

Status:

Tags: [[React]] [[React Router]]

---
# React Router 6
https://reactrouter.com/6.30.1/start/tutorial

## What is the difference between react-router and react-router-dom [^1]
  
React router (previously) had 2 different versions: dom for web and native for mobile. With v7, they dropped native and the “react-router-dom” name in favor of simply “react-router”.

There is still a v7 version of react-router-dom that is the same as react-router, but it should only be used for upgrading from v6. Once you’re done upgrading, you should change all of your import statements and use react-router.


---
## Different Routers [^2] 
1. BrowserRouter
2. HashRouter
3. MemoryRouter
4. StaticRouter
5. **createBrowserRouter / RouterProvider** (Data Router API)
### 📦 Summary Table

| Router                                   | Use Case                              | URL Type   | SSR Support        |
| ---------------------------------------- | ------------------------------------- | ---------- | ------------------ |
| `BrowserRouter`                          | Standard web apps                     | Clean URLs | ❌                  |
| `HashRouter`                             | Static hosting without server routing | Hash URLs  | ❌                  |
| `MemoryRouter`                           | Tests, non-DOM (e.g., React Native)   | None       | ❌                  |
| `StaticRouter`                           | Server-side rendering                 | Manual     | ✅                  |
| `createBrowserRouter` + `RouterProvider` | \|Data APIs & nested routing\|<br>    | Clean URLs | ✅ (with SSR setup) |

---
## Adding a Router
First thing to do is create a [Browser Router](https://reactrouter.com/6.30.1/routers/create-browser-router) and configure our first route. This will enable client side routing for our web app.

The `main.jsx` file is the entry point. Open it up and we'll put React Router on the page.

👉 **Create and render a [browser router](https://reactrouter.com/6.30.1/routers/create-browser-router) in `main.jsx`**

```jsx
import * as React from "react";
import * as ReactDOM from "react-dom/client";
import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";
import "./index.css";

const router = createBrowserRouter([
  {
    path: "/",
    element: <div>Hello world!</div>,
  },
]);

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```

This first route is what we often call the "root route" since the rest of our routes will render inside of it. It will serve as the root layout of the UI, we'll have nested layouts as we get farther along.

## Handling Not Found Errors

It's always a good idea to know how your app responds to errors early in the project because we all write far more bugs than features when building a new app! Not only will your users get a good experience when this happens, but it helps you during development as well.

Anytime your app throws an error while rendering, loading data, or performing data mutations, React Router will catch it and render an error screen. Let's make our own error page.
```jsx
import { useRouteError } from "react-router-dom";

export default function ErrorPage() {
  const error = useRouteError();
  console.error(error);

  return (
    <div id="error-page">
      <h1>Oops!</h1>
      <p>Sorry, an unexpected error has occurred.</p>
      <p>
        <i>{error.statusText || error.message}</i>
      </p>
    </div>
  );
}

```

```jsx
/* previous imports */
import ErrorPage from "./error-page";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
  },
]);

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);

```

Note that [`useRouteError`](https://reactrouter.com/6.30.1/hooks/use-route-error) provides the error that was thrown. When the user navigates to routes that don't exist you'll get an [error response](https://reactrouter.com/6.30.1/utils/is-route-error-response) with a "Not Found" `statusText`. 
## Nested Routes

We want the contact component to render _inside_ of the `<Root>` layout like this.

![](https://reactrouter.com/_docs/tutorial/05.webp)

We do it by making the contact route a _child_ of the root route.

👉 **Move the contacts route to be a child of the root route**
```jsx
const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
    children: [
      {
        path: "contacts/:contactId",
        element: <Contact />,
      },
    ],
  },
]);

```

You'll now see the root layout again but a blank page on the right. We need to tell the root route _where_ we want it to render its child routes. We do that with [`<Outlet>`](https://reactrouter.com/6.30.1/components/outlet).
## Client Side Routing

You may or may not have noticed, but when we click the links in the sidebar, the browser is doing a full document request for the next URL instead of using React Router.

Client side routing allows our app to update the URL without requesting another document from the server. Instead, the app can immediately render new UI. Let's make it happen with [`<Link>`](https://reactrouter.com/6.30.1/components/link).

👉 **Change the sidebar `<a href>` to `<Link to>`**
```jsx
<Link to={`contacts/2`}>Your Friend</Link>
```

## Loading Data

URL segments, layouts, and data are more often than not coupled (tripled?) together. We can see it in this app already:

|URL Segment|Component|Data|
|---|---|---|
|/|`<Root>`|list of contacts|
|contacts/:id|`<Contact>`|individual contact|

Because of this natural coupling, React Router has data conventions to get data into your route components easily.

There are two APIs we'll be using to load data, [`loader`](https://reactrouter.com/6.30.1/route/loader) and [`useLoaderData`](https://reactrouter.com/6.30.1/hooks/use-loader-data). First we'll create and export a loader function in the root module, then we'll hook it up to the route. Finally, we'll access and render the data.
👉 **Export a loader from `root.jsx`**

```jsx
// root.jsx -> Doesn't need to be here
export async function loader() { 
	const contacts = await getContacts();
	return { contacts }; 
}
```

👉 **Configure the loader on the route**

```jsx
/* other imports */
import Root, { loader as rootLoader } from "./routes/root";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
    loader: rootLoader,
    children: [
      {
        path: "contacts/:contactId",
        element: <Contact />,
      },
    ],
  },
]);
```

👉 **Access and render the data**

```jsx
// root.jsx
import {
  Outlet,
  Link,
  useLoaderData,
} from "react-router-dom";
import { getContacts } from "../contacts";

/* other code */

export default function Root() {
  const { contacts } = useLoaderData();
  return (
        {/* View code */}
  );
}
```
That's it! React Router will now automatically keep that data in sync with your UI

## Data Writes + HTML Forms

React Router emulates HTML Form navigation as the data mutation primitive, according to web development before the JavaScript cambrian explosion. It gives you the UX capabilities of client rendered apps with the simplicity of the "old school" web model.

While unfamiliar to some web developers, **`HTML forms actually cause a navigation in the browser, just like clicking a link`**. The only difference is in the request: standard links can only change the URL while forms can also change the request method (GET vs POST) and the request body (POST form data).

Without client side routing, the browser will serialize the form's data automatically and send it to the server as the request body for POST, and as URLSearchParams for GET. **`React Router does the same thing, except instead of sending the request to the server, it uses client side routing and sends it to a route "action"`** [`action`](https://reactrouter.com/6.30.1/route/action).

 [`<Form>`](https://reactrouter.com/6.30.1/components/form) prevents the browser from sending the request to the server and sends it to your route `action` instead. In web semantics, a POST usually means some data is changing. By convention, React Router uses this as a hint to automatically revalidate the data on the page after the action finishes. That means all of your `useLoaderData` hooks update and the UI stays in sync with your data automatically! Pretty cool.

## URL Params in Loaders
 the URL now has a real ID for the record.
![](https://reactrouter.com/_docs/tutorial/09.webp)
Reviewing the route config, the route looks like this:

```jsx
[
  {
    path: "contacts/:contactId",
    element: <Contact />,
  },
];
```

Note the `:contactId` URL segment. The colon (`:`) has special meaning, turning it into a "dynamic segment". Dynamic segments will match dynamic (changing) values in that position of the URL, like the contact ID. We call these values in the URL "URL Params", or just "params" for short.

These [`params`](https://reactrouter.com/6.30.1/route/loader#params) are passed to the loader with keys that match the dynamic segment. For example, our segment is named `:contactId` so the value will be passed as `params.contactId`.

These params are most often used to find a record by ID. Let's try it out.

👉 **Add a loader to the contact page and access data with `useLoaderData`**

```jsx
import { Form, useLoaderData } from "react-router-dom";
import { getContact } from "../contacts";

export async function loader({ params }) {
  const contact = await getContact(params.contactId);
  return { contact };
}

export default function Contact() {
  const { contact } = useLoaderData();
  // existing code
}
```

👉 **Configure the loader on the route**

```jsx
/* existing code */
import Contact, {
  loader as contactLoader,
} from "./routes/contact";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
    loader: rootLoader,
    action: rootAction,
    children: [
      {
        path: "contacts/:contactId",
        element: <Contact />,
        loader: contactLoader,
      },
    ],
  },
]);

/* existing code */
```

## Accessing Form Data

Just like creating data, you update data with [`<Form>`](https://reactrouter.com/6.30.1/components/form).

The edit route we just created already renders a form. All we need to do to update the record is wire up an action to the route. The form will post to the action and the data will be automatically revalidated.
```jsx
// edit.jsx
import {
  Form,
  useLoaderData,
  redirect,
} from "react-router-dom";
import { updateContact } from "../contacts";

export async function action({ request, params }) {
  const formData = await request.formData();
  const updates = Object.fromEntries(formData);
  await updateContact(params.contactId, updates);
  return redirect(`/contacts/${params.contactId}`);
}

export default function EditContact() {
  const { contact } = useLoaderData();

  return (
    <Form method="post" id="contact-form">
      <p>
        <span>Name</span>
        <input
          placeholder="First"
          aria-label="First name"
          type="text"
          name="first"
          defaultValue={contact?.first}
        />
        <input
          placeholder="Last"
          aria-label="Last name"
          type="text"
          name="last"
          defaultValue={contact?.last}
        />
      </p>
      <label>
        <span>Twitter</span>
        <input
          type="text"
          name="twitter"
          placeholder="@jack"
          defaultValue={contact?.twitter}
        />
      </label>
      <label>
        <span>Avatar URL</span>
        <input
          placeholder="https://example.com/avatar.jpg"
          aria-label="Avatar URL"
          type="text"
          name="avatar"
          defaultValue={contact?.avatar}
        />
      </label>
      <label>
        <span>Notes</span>
        <textarea
          name="notes"
          defaultValue={contact?.notes}
          rows={6}
        />
      </label>
      <p>
        <button type="submit">Save</button>
        <button type="button">Cancel</button>
      </p>
    </Form>
  );
}

```
Without JavaScript, when a form is submitted, the browser will create [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData) and set it as the body of the request when it sends it to the server. As mentioned before, React Router prevents that and sends the request to your action instead, including the [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData).

Each field in the form is accessible with `formData.get(name)`. For example, given the input field from above, you could access the first and last names like this:

```jsx
export async function action({ request, params }) {
  const formData = await request.formData();
  const firstName = formData.get("first");
  const lastName = formData.get("last");
  // ...
}
```
Since we have a handful of form fields, we used [`Object.fromEntries`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries) to collect them all into an object, which is exactly what our `updateContact` function wants.

```jsx
const updates = Object.fromEntries(formData);
updates.first; // "Some"
updates.last; // "Name"
```

After we finished the action, note the [`redirect`](https://reactrouter.com/6.30.1/fetch/redirect) at the end:

```jsx
  return redirect(`/contacts/${params.contactId}`);
```

Loaders and actions can both [return a `Response`](https://reactrouter.com/6.30.1/route/loader#returning-responses) (makes sense, since they received a [`Request`](https://developer.mozilla.org/en-US/docs/Web/API/Request)!). The [`redirect`](https://reactrouter.com/6.30.1/fetch/redirect) helper just makes it easier to return a [response](https://developer.mozilla.org/en-US/docs/Web/API/Response) that tells the app to change locations.

### `request` in Loader

This is a [Fetch Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) instance being made to your application.

```jsx
function loader({ request }) {}
```

> A request?!

It might seem odd at first that loaders receive a "request". Consider that `<Link>` does something like the following code and ask yourself, "what default behavior is being prevented here?".

```jsx
<a
  href={props.to}
  onClick={(event) => {
    event.preventDefault();
    navigate(props.to);
  }}
/>
```

Without React Router, the browser would have made a _Request_ to your server, but React Router prevented it! Instead of the browser sending the request to your server, React Router sends the request to your loaders.

The most common use case is creating a [URL](https://developer.mozilla.org/en-US/docs/Web/API/URL) and reading the [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) from it:

```jsx
function loader({ request }) {
  const url = new URL(request.url);
  const searchTerm = url.searchParams.get("q");
  return searchProducts(searchTerm);
}
```

Note that the APIs here are not React Router specific, but rather standard web objects: [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request), [URL](https://developer.mozilla.org/en-US/docs/Web/API/URL), [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams).

## Active Link Styling

Now that we have a bunch of records, it's not clear which one we're looking at in the sidebar. We can use [`NavLink`](https://reactrouter.com/6.30.1/components/nav-link) to fix this.

👉 **Use a `NavLink` in the sidebar**

```jsx
	<NavLink
	
	style={({ isActive, isPending }) =>
	
	  isActive ? linkStyle : {}
	
	}
	to={`contacts/${contact.id}`}	
>	
{children}
	
	</NavLink>
```

```jsx
	<NavLink
	
	to={`contacts/${contact.id}`}
	
	className={({ isActive, isPending }) =>
	
	  isActive ? "active" : isPending ? "pending" : ""
	
	}
	
>	
{children}
	
	</NavLink>
```
Note that we are passing a function to `className`. When the user is at the URL in the `NavLink`, then `isActive` will be true. When it's _about_ to be active (the data is still loading) then `isPending` will be true. This allows us to easily indicate where the user is, as well as provide immediate feedback on links that have been clicked but we're still waiting for data to load.

## useNavigation

As the user navigates the app, React Router will _leave the old page up_ as data is loading for the next page.

React Router is managing all of the state behind the scenes and reveals the pieces of it you need to build dynamic web apps. In this case, we'll use the [`useNavigation`](https://reactrouter.com/6.30.1/hooks/use-navigation) hook.
👉 **`useNavigation` to add global pending UI**

```jsx
import {
  // existing code
  useNavigation,
} from "react-router-dom";

// existing code

export default function Root() {
  const { contacts } = useLoaderData();
  const navigation = useNavigation();

  return (
    <>
      <div id="sidebar">{/* existing code */}</div>
      <div
        id="detail"
        className={
          navigation.state === "loading" ? "loading" : ""
        }
      >
        <Outlet />
      </div>
    </>
  );
}
```

[`useNavigation`](https://reactrouter.com/6.30.1/hooks/use-navigation) returns the current navigation state: it can be one of `"idle" | "submitting" | "loading"`.

## Rerouting through Link and Form 
Like `<Link to>`, `<Form action>` can take a _relative_ value. Since the form is rendered in `contact/:contactId`, then a relative action with `destroy` will submit the form to `contact/:contactId/destroy` when clicked.
```jsx
  <Form
	method="post"
	action="destroy"
	onSubmit={(event) => {
	  if (
		!confirm(
		  "Please confirm you want to delete this record."
		)
	  ) {
		event.preventDefault();
	  }
	}}
>
	<button type="submit">Delete</button>
  </Form>
```
When the user clicks the submit button:

1. `<Form>` prevents the default browser behavior of sending a new POST request to the server, but instead emulates the browser by creating a POST request with client side routing
2. The `<Form action="destroy">` matches the new route at `"contacts/:contactId/destroy"` and sends it the request
3. After the action redirects, React Router calls all of the loaders for the data on the page to get the latest values (this is "revalidation"). `useLoaderData` returns new values and causes the components to update!

Add a form, add an action, React Router does the rest.

### Why POST for `delete`button
In React Router, the `method` attribute on a `<Form>` component is crucial because it dictates how the form submission is handled and whether a data mutation (write) is intended.

Here's why `method="post"` is used for the "Delete" button but not for the "Edit" button in your provided code:

1. **Default Form Method (for "Edit" button):**
    
    - When no `method` attribute is explicitly specified on an HTML `<form>`, the **default method is `GET`**. React Router's `<Form>` component behaves similarly.
    - The "Edit" button's form, `<Form action="edit">`, lacks a `method` attribute. Therefore, it defaults to a `GET` submission.
    - This form's primary purpose at this point is to **navigate to the edit page** for the specific record. A `GET` request is appropriate for simply requesting a new page or loading data, much like clicking a link. It is not performing a data mutation directly from this button click. The tutorial shows that the actual form for _updating_ the contact data (on the `contacts/:contactId/edit` route) does use `method="post"`.
2. **Explicit `method="post"` (for "Delete" button):**
    
    - The "Delete" button's form, `<Form method="post" action="destroy">`, explicitly sets the `method` to `"post"`.
    - **`POST` is used for data mutations**—operations that change data on the server, such as creating, updating, or deleting records. Deleting a record is a destructive data write operation.
    - When a React Router `<Form>` uses `method="post"`, it prevents the default browser behavior and instead **sends the request to a route `action`** defined for that route. In the case of the "Delete" button, it targets the `contacts/:contactId/destroy` route's `action`.
    - After the `action` finishes (and typically redirects), React Router automatically **revalidates all loaders** on the page to fetch the latest data, ensuring the UI stays in sync. This is important for "Delete" because the list of contacts on the sidebar needs to update to reflect the deleted record.

In summary, the "Edit" button's form triggers a navigation to a page where editing can occur (a `GET` request to retrieve data), while the "Delete" button's form directly initiates a data change operation (a `POST` request to delete data).

## Contextual Errors
In React Router, a **contextual error** refers to an error that occurs within a specific route or a part of your application's UI, allowing for a more localized and user-friendly error display.

Here's a breakdown of what a contextual error entails and how it's handled:

- **Handling Specific Route Errors**:
    
    - Previously, the tutorial demonstrated a global `errorElement` on the root route that would catch any error across the application, leading to a full-page error display.
    - To make errors more contextual, you can define an `errorElement` directly on a specific child route. For example, if an error occurs in the `destroy` action of a specific contact route, you can configure that particular route to display a more specific error message.
- **User Experience Improvement**:
    
    - Instead of presenting a generic full-page error that forces the user to refresh, a contextual error allows only the affected part of the page to show an error message.
    - This approach **gives the user more options** to recover or continue interacting with the parts of the page that are not experiencing issues.
- **Error Bubbling**:
    
    - Errors in React Router **bubble up to the nearest `errorElement`**. This means if a child route has its own `errorElement`, any error within that child route (or its further nested children) will be caught and rendered by that specific `errorElement`, rather than by a parent or the root `errorElement`.
- **Pathless Routes for Shared Contextual Errors**:
    
    - When you want to apply the same `errorElement` to multiple child routes to ensure errors render inside a common parent outlet (like the root outlet), you can use a **pathless route**.


## URL Search Params and GET Submissions

The search field is interesting because it's a mix of both: it's a form but it only changes the URL, it doesn't change data.

Right now it's just a normal HTML `<form>`, not a React Router `<Form>`. Let's see what the browser does with it by default:

👉 **Type a name into the search field and hit the enter key**

Note the browser's URL now contains your query in the URL as [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams):

```
http://127.0.0.1:5173/?q=ryan
```

If we review the search form, it looks like this:

```jsx
<form id="search-form" role="search">
  <input
    id="q"
    aria-label="Search contacts"
    placeholder="Search"
    type="search"
    name="q"
  />
  <div id="search-spinner" aria-hidden hidden={true} />
  <div className="sr-only" aria-live="polite"></div>
</form>
```

As we've seen before, browsers can serialize forms by the `name` attribute of it's input elements. The name of this input is `q`, that's why the URL has `?q=`. If we named it `search` the URL would be `?search=`.

Note that this form is different from the others we've used, it does not have `<form method="post">`. The default `method` is `"get"`. That means when the browser creates the request for the next document, it doesn't put the form data into the request POST body, but into the [`URLSearchParams`](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) of a GET request.

## Get submissions with client side routing part

- **Default Behavior**: An HTML `<form>` without a specified `method` attribute defaults to the `GET` method. When submitted, the browser appends input values (using their `name` attributes) as `URLSearchParams` to the URL (e.g., `?q=searchterm`).
- **React Router's Role**: When using React Router's `<Form>` component for a `GET` submission, it **prevents the default browser behavior** of sending a new request to the server. Instead, it uses client-side routing to update only the URL, without a full page refresh.
- **No `action` Call**: For `GET` submissions, React Router **does not call a route `action`**. It treats a `GET` form submission similarly to clicking a link – the primary effect is a URL change.
- **Data Handling**: Any logic to process the form data (like filtering or searching) must be implemented in the **route's `loader` function**. The `loader` is automatically re-run when the URL's search parameters change, allowing it to access the query from `request.url` and filter data accordingly.
- **Benefits**: This approach allows for dynamic, interactive features like search and filtering while maintaining client-side routing advantages such as faster UI updates and manipulation of the browser history stack.

## useSubmit
https://reactrouter.com/6.30.1/hooks/use-submit
`useSubmit` is a React Router hook that allows you to programmatically submit forms.

Here's a summary of its key aspects:
- **Purpose**: It's used when you want a form to be submitted on an event other than a standard form submission (e.g., automatically as a user types in a search field via an `onChange` event).
- **Usage**:
    - You import `useSubmit` from `react-router-dom` and call it within your component to get a `submit` function: `const submit = useSubmit();`.
    - The `submit` function takes a form DOM node as an argument (e.g., `event.currentTarget.form`), which it then serializes and submits.
- **Effect**: When `submit` is called with a form, it triggers the associated route `action` (for `POST` methods) or `loader` (for `GET` methods) and handles client-side routing and data revalidation, similar to a `<Form>` component.
- **History Management**: For frequent submissions (like on every keystroke), using `submit` can create many entries in the browser's history stack. To avoid this, you can pass an options object to `submit` with `replace: true` to replace the current history entry instead of adding a new one. For example: `submit(event.currentTarget.form, { replace: !isFirstSearch });`.


## Managing the History Stack

Now that the form is submitted for every key stroke, if we type the characters "seba" and then delete them with backspace, we end up with 7 new entries in the stack 😂. We definitely don't want this

![](https://reactrouter.com/_docs/tutorial/23.webp)

We can avoid this by _replacing_ the current entry in the history stack with the next page, instead of pushing into it.

👉 **Use `replace` in `submit`**

```jsx
// existing code

export default function Root() {
  // existing code

  return (
            <input
              id="q"
              // existing code
              onChange={(event) => {
                const isFirstSearch = q == null;
                submit(event.currentTarget.form, {
                  replace: !isFirstSearch,
                });
              }}
            />
  );
}
```

We only want to replace search results, not the page before we started searching, so we do a quick check if this is the first search or not and then decide to replace.

Each key stroke no longer creates new entries, so the user can click back out of the search results without having to click it 7 times 😅.

## useFetcher()
https://reactrouter.com/6.30.1/hooks/use-fetcher

`useFetcher` is a React Router hook designed for performing data mutations (communicating with loaders and actions) **without causing a navigation**.

Here are its key characteristics:

- **Purpose**
    
    - Allows you to change data on the server without changing the current page or affecting the browser's history stack.
    - Ideal for scenarios where you want to update a small piece of data on the current view, such as a "favorite" button.
- **Usage**
    
    - You use `useFetcher()` to obtain a `fetcher` object.
    - Instead of a standard `<Form>` component, you use `<fetcher.Form>`.
    - `<fetcher.Form>` functions similarly to `<Form>`, typically using `method="post"` to call a route `action`.
    - If no `action` prop is provided to `<fetcher.Form>`, it posts to the action of the route where it is rendered.
- **Behavior**
    
    - When a `<fetcher.Form>` is submitted, it calls the associated route `action` (for `POST`) or `loader` (for `GET`).
    - After the action or loader finishes, React Router **automatically revalidates all data** on the page, ensuring `useLoaderData` hooks update and the UI stays in sync.
    - Errors in `fetcher` actions are caught and handled in the same way as regular `Form` submissions.
    - The crucial difference from a regular `<Form>` is that **the URL does not change**, and the browser's history stack remains unaffected.
- **Optimistic UI**
    
    - `useFetcher` supports building optimistic UI by providing access to `fetcher.state` (similar to `navigation.state`) and `fetcher.formData`.
    - `fetcher.formData` contains the data currently being submitted, allowing you to immediately update the UI with the _anticipated_ new state before the server response is received.
    - Once the action is complete, `fetcher.formData` becomes unavailable, and the UI reverts to displaying the actual data returned from the server.


## Optmistic UI
**Optimistic UI** is a strategy used in React Router to enhance user experience by providing immediate feedback for actions, especially during network latency.

Here's how it works:

- **Immediate Feedback**: The UI is updated instantly with the _anticipated_ new state of the data, even before the server response is received.
- **`fetcher.formData`**: It utilizes `fetcher.formData` (available from the `useFetcher` hook), which holds the data currently being submitted to an action. This allows the UI to reflect the pending changes immediately.
- **Reversion on Completion**: Once the server-side action completes (or if it fails), `fetcher.formData` becomes unavailable. The UI then reverts to displaying the actual data returned from the server, ensuring data consistency.
- **Improved Responsiveness**: This technique makes the application feel more responsive by eliminating perceived delays between user action and UI update.

## pathlesss Routes
**Pathless routes** in React Router are a mechanism to participate in UI layout without requiring new path segments in the URL.

Here's a summary:

- **Definition**: A route defined without a `path` attribute.
- **Purpose**: Allows routes to contribute to the UI layout or error handling for their children without altering the URL.
- **Key Use Case (Contextual Errors)**: They are particularly useful for catching errors from multiple child routes to render an `errorElement` within a common parent outlet (like the root outlet).
- **Benefit for Errors**: This ensures that when an error occurs in a child route, only the affected section of the page displays the error, preserving the main UI of the parent route and offering users more recovery options than a full-page error.
- **Configuration**: To implement, child routes are wrapped within a pathless route that defines an `errorElement`.


## JSX Routes

And for our final trick, many folks prefer to configure their routes with JSX. You can do that with `createRoutesFromElements`. There is no functional difference between JSX or objects when configuring your routes, it's simply a stylistic preference.

```jsx
import {
  createRoutesFromElements,
  createBrowserRouter,
  Route,
} from "react-router-dom";

const router = createBrowserRouter(
  createRoutesFromElements(
    <Route
      path="/"
      element={<Root />}
      loader={rootLoader}
      action={rootAction}
      errorElement={<ErrorPage />}
    >
      <Route errorElement={<ErrorPage />}>
        <Route index element={<Index />} />
        <Route
          path="contacts/:contactId"
          element={<Contact />}
          loader={contactLoader}
          action={contactAction}
        />
        <Route
          path="contacts/:contactId/edit"
          element={<EditContact />}
          loader={contactLoader}
          action={editAction}
        />
        <Route
          path="contacts/:contactId/destroy"
          action={destroyAction}
        />
      </Route>
    </Route>
  )
);
```

Copy code to clipboard



---
## Rough from Scrimba Course
- BrowserRouter is a Context Provider. So, We need to wrap the entire component around it.
- Routes 
- Route

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom"
ReactDOM.createRoot(document.getElementById('root')).render(

  <BrowserRouter>

    <Routes>

    </Routes>

  </BrowserRouter>

);
```

- we need to have a way to change paths to different paths without refreshing - `link`

```jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom"
<nav>

  <Link to="/about">About</Link>

</nav>
```

Nested Routes, Route parameters
- Route params? why it is useful?  
-  useParams() -> to get params
- nested rotes contain shared UI
![[Pasted image 20250823162521.png]]

Layout Routes
- <Layout />
- Outlet
- Relative paths
- Index Routes -> `index` mean default

```jsx
//Layout
import React from "react"

import { Outlet } from "react-router-dom"

import Header from "./Header"

export default function Layout() {

    return (

        <>

            <Header />

            <Outlet />

        </>

    )

}

```


---
1. What is the primary reason to use a nested route?
Whenever we have some shared UI between routes in our app.

2. What is a "Layout Route"?
It's the parent route of some nested routes that contains just
the portion of the UI that will be shared. It will use an Outlet
component.

3. What does the <Outlet /> component do? When do you use it?
We use it anytime we have a parent Route that's wrapping
children routes. It renders the matching child route's
`element` prop given in its route definition

4. What is an "Index Route"?
It's the "default route" we want to render when the path
of the parent route matches. It gives us a chance to render
an element inside the parent's <Outlet /> at the same path
as the parent route.

---
NavLink
- cllassName
- style
- end - end the matching here
Relative links (different from relative links)
- relative="path" 
```jsx
<Link
	to=".."
	relative="path"
	className="back-button"
>&larr; <span>Back to all vans</span>
</Link>
```

---
useOutletContext

Query Parameters 
- single source of truth
- Represent a change in the UI
	- Sorting, filtering, pagination
- key/value pairs in the URL
- useSearchParams
- searchParams.get("type")
- different ways to set search params
	- using link
	- using button -> setSearchParam(string or object)
- Merging search params with Links
```jsx
 function genNewSearchParamString(key, value) {

    const sp = new URLSearchParams(searchParams)

    if (value === null) {

      sp.delete(key)

    } else {

      sp.set(key, value)

    }

    return `?${sp.toString()}`

  }
```

how to keep reference of previous page or parent route filters?
- `state` in link
	- The `state` property can be used to set a stateful value for the new location which is stored inside [history state](https://developer.mozilla.org/en-US/docs/Web/API/History/state). This value can subsequently be accessed via `useLocation()`.

- The term "location" in React Router refers to [the `Location` interface](https://github.com/remix-run/history/blob/main/docs/api-reference.md#location) from the [history](https://github.com/remix-run/history) library.

404 page:
catch all route
```jsx
<Route path="*" element={<h1>Page not found!</h1>} />
```
- In the new version, it doesn't matter if you put it first or last.

Happy path vs sad path
![[Pasted image 20250827151302.png]]
![[Pasted image 20250827151235.png]]

---
### Protected routes

![[Pasted image 20250827172412.png]]
![[Pasted image 20250827172439.png]]
- `<Navigate>` 
```jsx
import React from "react"
import { Outlet, Navigate } from "react-router-dom"

export default function AuthRequired() {
    const authenticated = false
    if (!authenticated) {
        return <Navigate to="/login" />
    }

    return <Outlet />
}
```

```jsx
    <BrowserRouter>

      <Routes>

        <Route path="/" element={<Layout />}>

          <Route index element={<Home />} />

          <Route path="about" element={<About />} />

          <Route path="vans" element={<Vans />} />

          <Route path="vans/:id" element={<VanDetail />} />

          <Route

            path="login"

            element={<Login />}

          />

  

          <Route element={<AuthRequired />}>

            <Route path="host" element={<HostLayout />}>

              <Route index element={<Dashboard />} />

              <Route path="income" element={<Income />} />

              <Route path="reviews" element={<Reviews />} />

              <Route path="vans" element={<HostVans />} />

              <Route path="vans/:id" element={<HostVanDetail />}>

                <Route index element={<HostVanInfo />} />

                <Route path="pricing" element={<HostVanPricing />} />

                <Route path="photos" element={<HostVanPhotos />} />

              </Route>

            </Route>

          </Route>

  

          <Route path="*" element={<NotFound />} />

        </Route>

      </Routes>

    </BrowserRouter>
```
- usenavigate()
- History stack and replace
```jsx
export default function AuthRequired() {

    const isLoggedIn = localStorage.getItem("loggedin")

    if (!isLoggedIn) {

        return (

            <Navigate

                to="/login"

                state={{message: "You must log in first"}}

                replace={true}

            />)

    }

    return <Outlet />

}
```

- useLocation
---
## Relevant Links
https://reactrouter.com/6.30.1/components/link#state
https://reactrouter.com/6.30.1/hooks/use-outlet-context
https://reactrouter.com/6.30.1/hooks/use-search-params
https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams#urlsearchparamssymbol.iterator
https://reactrouter.com/6.30.1/hooks/use-location#uselocation
https://reactrouter.com/6.30.1/hooks/use-navigate#usenavigate
https://reactrouter.com/6.30.1/hooks/use-location
https://reactrouter.com/6.30.1/route/error-element#errorelement
https://reactrouter.com/6.30.1/hooks/use-route-error
https://developer.mozilla.org/en-US/docs/Web/API/Response
https://reactrouter.com/6.30.1/route/loader
https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams#urlsearchparamssymbol.iterator
https://developer.mozilla.org/en-US/docs/Web/API/URL/searchParams
https://reactrouter.com/6.30.1/hooks/use-location#properties

---
## References
[[Single Page Vs multipage Applications]]
[[Deploy to Netlifly]]
[[Mirage JS]]
[[Using fetch() in React]]
[[Loaders and actions - React Router]]
[^1]: [[React Router 6 vs 7]]
[^2]: [[How to pick a Router - React Router 6]]









