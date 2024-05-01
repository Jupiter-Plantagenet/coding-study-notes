Components
Components are the building blocks of UI in react. A UI is one or more components combined. Components are self contained, with their own logic, data and appearance. Programmatically, they are JS functions which start with capital letters and return a single jsx element.
- All component declarations must be top level
- You write JS logic in jsx in `{}`

## Handling Events
Here's how event handling works in React using functional components:

**1. Event Bindings:**

   - You attach event handlers to React elements using JSX syntax. Event handlers are defined as functions within your component.
   - Event handlers are passed as props to the element within curly braces `{}` after the attribute name. For example:
     ```jsx
     <button onClick={handleClick}>Click Me</button>
     ```

**2. Event Handlers:**

   - Event handlers are functions that define the code to be executed when a specific event occurs on an element. These functions receive an event object as an argument, containing information about the event.

**3. State Updates:**

   - Functional components don't have direct access to state like class components. To manage state in functional components, you use the `useState` hook provided by React.
   - `useState` returns an array with two elements: the current state value and a function to update it. You can call the update function (often named `setState`) within your event handler to modify the state.

Here's an example of a functional React component that handles a click event and updates state using the `useState` hook:

```jsx
import { useState } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount(count + 1);
  }

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={handleClick}>Click me</button>
    </div>
  );
}
```

In this example:

- The component uses the `useState` hook to create a state variable `count` with an initial value of 0.
- The `handleClick` function is the event handler for the button click.
- When the button is clicked, `handleClick` is called.
- Inside `handleClick`, the state is updated using `setCount(count + 1)`, which triggers a re-render of the component with the updated `count` value.
You're right, I missed discussing preventing default behavior in the previous explanation. Here's how you can prevent default behavior in React functional components using event handlers:

**4. Preventing Default Behavior:**

- Sometimes, you might want to prevent the default behavior of an event. For example, clicking a submit button (`<button type="submit">`) within a form would cause a full page reload by default.
- You can use the `event.preventDefault()` method inside your event handler to stop this default behavior.

Here's the updated example incorporating preventing default behavior:

```jsx
import { useState } from 'react';

function MyForm() {
  const [name, setName] = useState('');

  const handleSubmit = (event) => {
    event.preventDefault(); // Prevent default form submission behavior
    console.log('Form submitted:', name);
    // Handle form submission logic here (e.g., send data to server)
    setName(''); // Reset form after submission (optional)
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={name} onChange={(e) => setName(e.target.value)} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}
```

In this example:

- The component defines a form with a name input and a submit button.
- The `handleSubmit` function is the event handler for the form submission (`onSubmit`).
- Inside `handleSubmit`, we call `event.preventDefault()` to prevent the default form submission behavior (reloading the page).
- The form submission logic can then be implemented here, such as logging the data to the console or sending it to a server.

Remember, using `event.preventDefault()` is only necessary when you want to handle the form submission yourself within your React application and prevent the default behavior.
---
## List and Keys
In React, lists and keys are essential concepts for rendering collections of elements efficiently and uniquely. Here's a breakdown of what they are and how they work together:

**1. Lists:**

- In React, you often work with collections of data, such as arrays of objects representing users, products, or any other kind of item.
- You can display these lists of data in your user interface (UI) using JSX syntax and looping through the data. For example:

```jsx
const numbers = [1, 2, 3, 4, 5];

return (
  <ul>
    {numbers.map((number) => (
      <li key={number}>{number}</li>
    ))}
  </ul>
);
```

- In this example, the `numbers` array is iterated over using the `map` function. Inside the `map` function, an `li` element is created for each number in the list.

**2. Keys:**

   - Keys are unique identifiers assigned to each item in a list. They are used by React to efficiently identify which items have changed, been added, or removed when the data underlying the list changes.
   - Keys are essential for performance optimization and maintaining a consistent UI state.
   - Keys are specified within the JSX element using the `key` attribute. It should be a unique identifier for that specific item within the list. Ideally, the key should be a unique property from your data (e.g., an ID from a database).

**Why Keys are Important:**

   - Without keys, React might re-render the entire list even if only a single item changes. This can be inefficient, especially for large lists.
   - Keys help React determine which items need to be updated, added, or removed when the data changes. This ensures an optimal rendering process and avoids unnecessary re-renders.

**Best Practices for Keys:**

   - Keys should be unique among siblings within the list. It's okay to have duplicate keys across different lists.
   - In most cases, the best key is a unique identifier from your data (e.g., an ID field in a database record).
   - If you don't have a natural unique identifier, you can resort to using the index of the item within the array as a last resort. However, this is not ideal as reordering the list would cause React to re-render all items.

**Example: Updating a List:**

Imagine you have a list of users and their names. If a user's name changes, you would update the data and re-render the list. With keys:

1. React can identify the specific user that changed based on the key.
2. It only re-renders the element associated with the changed user, keeping other elements intact.

Without keys, React might not be able to efficiently determine which user has changed and potentially re-render the entire list, leading to performance issues.

By effectively using lists and keys together, you can create dynamic and performant React applications that can efficiently handle and display collections of data.
---
## Generating stable, unique keys with uuid package
Here's how you can use the `uuid` package to maintain unique and consistent keys in React:

**1. Installation:**

  You'll need to install the `uuid` package using npm or yarn:

  ```bash
  npm install uuid
  ```

**2. Importing the Library:**

  Import the `v4` function (which generates version 4 UUIDs) from the `uuid` package in your React component:

  ```javascript
  import { v4 as uuidv4 } from 'uuid';
  ```

**3. Generating UUIDs for Keys:**

  Use the `uuidv4` function to generate a unique identifier (UUID) for each item in your list. You do this at the data level **NOT** at the UI/render level:

  ```jsx
  const users = [
    { id : uuidv4(), name: 'Alice' },
    { id : uuidv4(), name: 'Bob' },
    { id : uuidv4(), name: 'Charlie' },
  ];

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
  ```

  In this example:

  - We use `uuidv4()` to generate a unique identifier (UUID) for each user object at the data level
  - This id is then assigned to the `key` attribute of the `li` element.

**Important Considerations:**
- It's generally recommended to use unique identifiers from your data source (e.g., database IDs) as keys whenever possible. They are guaranteed to be unique within your data and offer better performance compared to UUIDs.
- Only use UUIDs as keys when a unique identifier isn't readily available from your data.
- Keys serve as a hint to React but they don’t get passed to your components. If you need the same value in your component, pass it explicitly as a prop with a different name:
  ```
  const content = posts.map((post) =>
  <Post
    key={post.id}
    id={post.id}
    title={post.title} />
);
  ```
With the example above, the Post component can read props.id, but not props.key.
---
## `map() and filter()`
Both `map()` and `filter()` are built-in methods in JavaScript that are commonly used for working with arrays. Here's a breakdown of what each method does:

**1. map():**

   - **Purpose:** Creates a new array by applying a function to each element of the original array.
   - **Syntax:**

     ```javascript
     const newArray = originalArray.map(function(currentValue, index, arr) {
       // transformation logic using currentValue, index (optional), and arr (optional)
       return transformedValue;
     });
     ```

   - **Parameters:**
     - `currentValue`: The element currently being processed in the loop.
     - `index` (optional): The index of the current element within the original array.
     - `arr` (optional): The original array being looped through.
   - **Return Value:** A new array containing the transformed elements.

   **Example:**

     ```javascript
     const numbers = [1, 2, 3, 4, 5];
     const doubledNumbers = numbers.map(number => number * 2);
     console.log(doubledNumbers); // Output: [2, 4, 6, 8, 10]
     ```

     In this example, the `map` function iterates over the `numbers` array and doubles each element. The resulting `doubledNumbers` array contains the transformed values.

**2. filter():**

   - **Purpose:** Creates a new array containing only elements from the original array that pass a test implemented by the provided function.
   - **Syntax:**

     ```javascript
     const filteredArray = originalArray.filter(function(currentValue, index, arr) {
       // filtering logic using currentValue, index (optional), and arr (optional)
       return booleanValue;
     });
     ```

   - **Parameters:** Similar to `map()`, it accepts `currentValue`, `index` (optional), and `arr` (optional) as arguments.
   - **Return Value:** A new array containing only the elements that passed the test defined in the function.

   **Example:**

     ```javascript
     const numbers = [1, 2, 3, 4, 5];
     const evenNumbers = numbers.filter(number => number % 2 === 0);
     console.log(evenNumbers); // Output: [2, 4]
     ```

     In this example, the `filter` function iterates over the `numbers` array and keeps only the elements that are even numbers (those that leave no remainder when divided by 2). The resulting `evenNumbers` array contains only the even elements from the original array.

**Key Differences:**

- `map()` transforms each element and creates a new array with the transformed values, regardless of whether the element meets a specific condition.
- `filter()` creates a new array containing only elements that fulfill a certain criteria defined in the provided function.
---

## Controlled Components
In React, Controlled Components are those in which form’s data is handled by the component’s state. It takes its current value through props and makes changes through callbacks like onClick, onChange, etc. A parent component manages its own state and passes the new values as props to the controlled component.

Example:
```
// FileName - App.js

import { useState } from "react";
import "./App.css";

function App() {
	const [name, setName] = useState("");

	function handleSubmit() {
		alert(`Name: ${name}`);
	}

	return (
		<div className="App">
			<h1 className="geeks">GeeksForGeeks</h1>
			<h3>Controlled Component</h3>
			<form onSubmit={handleSubmit}>
				<label>Name:</label>
				<input
					name="name"
					value={name}
					onChange={(e) =>
						setName(e.target.value)
					}
				/>
				<button type="submit">Submit</button>
			</form>
		</div>
	);
}

export default App;
```
This code defines a React component named `App` that demonstrates a controlled component for handling form input. Here's a breakdown of what each part does:

**1. Imports:**

   - `useState` hook is imported from `react` to manage component state.
   - `./App.css` is imported, likely containing styles for the component (not shown in this code snippet).

**2. `App` Function:**

   - This function defines the React component named `App`.

**3. State Management:**

   - `const [name, setName] = useState("");`
     - This line uses the `useState` hook to create a state variable named `name` with an initial value of an empty string (`""`).
     - The `setName` function is used to update the `name` state variable.

**4. `handleSubmit` Function:**

   - `function handleSubmit() { ... }`
     - This function is called when the form is submitted.
     - Inside the function:
       - `alert(`Name: ${name}`);`
         - An alert message is displayed with the current value of the `name` state variable, indicating the submitted name.

**5. JSX Return:**

   - The `return` statement defines what the component will render in the UI.
     - `<div className="App"> ... </div>`:
       - A `div` element with the class name `"App"` is the container for the form.

**6. Form Definition:**

     - `<h1>GeeksForGeeks</h1>`: Displays a heading with the text "GeeksForGeeks".
     - `<h3>Controlled Component</h3>`: Displays a subheading indicating the type of component (controlled component).
     - `<form onSubmit={handleSubmit}> ... </form>`:
       - A form element with the `onSubmit` event handler set to the `handleSubmit` function. This ensures the function is called when the form is submitted.

**7. Input Field:**

     - `<label>Name:</label>`: Displays a label for the name input field.
     - `<input ... />`: Defines the input element for user input.
       - `name="name"`: Sets the name attribute of the input field.
       - `value={name}`: Binds the value of the input field to the `name` state variable. This ensures the displayed value reflects the current state.
       - `onChange={(e) => setName(e.target.value)}`: Defines the `onChange` event handler for the input field. When the value changes:
         - `(e)` represents the event object.
         - `e.target.value` accesses the new value entered by the user.
         - The `setName` function is called with the new value, updating the state and consequently the displayed value of the input field.

**8. Submit Button:**

     - `<button type="submit">Submit</button>`: Defines a submit button that triggers form submission when clicked.

**9. Export:**

   - `export default App;`
     - This line exports the `App` component as the default export from this module, allowing other parts of your application to import and use it.

In summary, this code demonstrates a controlled component in React. The `name` state variable holds the user-entered name, and the input field's value is synchronized with the state. When the form is submitted, the `handleSubmit` function displays an alert with the submitted name.

## Use Formik to implement forms in react.
Formik is a small group of React components and hooks for building forms in React and React Native. It helps with the these:
1. Getting values in and out of form state
2. Validation and error messages
3. Handling form submission

### Part 1: useFormik() + Custom Validation Logic
We pass our form’s initialValues and a submission function (onSubmit) to the useFormik() hook. The hook then returns to us a goodie bag of form state and helper methods in a variable we call formik. For now, the only helper methods we care about are as follows:
- handleSubmit: A submission handler
- handleChange: A change handler to pass to each <input>, <select>, or <textarea>
- values: Our form’s current values
```
import React from "react";
import { useFormik } from "formik";

// A custom validation function. This must return an object
// which keys are symmetrical to our values/initialValues
const validate = (values) => {
  const errors = {};
  if (!values.firstName) {
    errors.firstName = "Required";
  } else if (values.firstName.length > 15) {
    errors.firstName = "Must be 15 characters or less";
  }

  if (!values.lastName) {
    errors.lastName = "Required";
  } else if (values.lastName.length > 20) {
    errors.lastName = "Must be 20 characters or less";
  }

  if (!values.email) {
    errors.email = "Required";
  } else if (!/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i.test(values.email)) {
    errors.email = "Invalid email address";
  }

  return errors;
};

export const SignupForm = () => {
  // Pass the useFormik() hook initial form values and a submit function that will
  // be called when the form is submitted
  const formik = useFormik({
    initialValues: {
      firstName: "",
      lastName: "",
      email: "",
    },
    validate,
    onSubmit: (values) => {
      alert(JSON.stringify(values, null, 2));
    },
  });
  return (
    <form onSubmit={formik.handleSubmit}>
      <label htmlFor="firstName">First Name</label>
      <input
        id="firstName"
        name="firstName"
        type="text"
        onChange={formik.handleChange}
        onBlur={formik.handleBlur}
        value={formik.values.firstName}
      />
      {
      //with touched, formik tracks which fields have been visited
      formik.touched.firstName && formik.errors.firstName ? (
        <div>{formik.errors.firstName}</div>
      ) : null}

      <label htmlFor="lastName">Last Name</label>
      <input
        id="lastName"
        name="lastName"
        type="text"
        onChange={formik.handleChange}
        onBlur={formik.handleBlur}
        value={formik.values.lastName}
      />
      {//with touched, formik tracks which fields have been visited
      formik.touched.lastName && formik.errors.lastName ? (
        <div>{formik.errors.lastName}</div>
      ) : null}

      <label htmlFor="email">Email Address</label>
      <input
        id="email"
        name="email"
        type="email"
        onChange={formik.handleChange}
        onBlur={formik.handleBlur}
        value={formik.values.email}
      />
      {//with touched, formik tracks which fields have been visited
      formik.touched.email && formik.errors.email ? (
        <div>{formik.errors.email}</div>
      ) : null}

      <button type="submit">Submit</button>
    </form>
  );
};

```


### Part 2: useFormik() + Yup
```
import React from "react";
import { useFormik } from "formik";
import * as Yup from "yup";

export const SignupForm = () => {
  // Pass the useFormik() hook initial form values and a submit function that will
  // be called when the form is submitted
  const formik = useFormik({
    initialValues: {
      firstName: "",
      lastName: "",
      email: "",
    },
    validationSchema : Yup.object({
      //validiation logic written using Yup methods
      firstName: Yup.string()
        .max(15, 'Must be 15 characters or less')
        .required('Required'),
      lastName: Yup.string()
        .max(20, 'Must be 20 characters or less')
        .required('Required'),
      email: Yup.string().email('Invalid email address').required('Required'),
    }),
    onSubmit: (values) => {
      alert(JSON.stringify(values, null, 2));
    },
  });
  return (
    <form onSubmit={formik.handleSubmit}>
      <label htmlFor="firstName">First Name</label>
      <input
        id="firstName"
        name="firstName"
        type="text"
        onChange={formik.handleChange}
        onBlur={formik.handleBlur}
        value={formik.values.firstName}
      />
      
      {//with touched, formik tracks which fields have been visited
      formik.touched.firstName && formik.errors.firstName ? (
        <div>{formik.errors.firstName}</div>
      ) : null}

      <label htmlFor="lastName">Last Name</label>
      <input
        id="lastName"
        name="lastName"
        type="text"
        onChange={formik.handleChange}
        onBlur={formik.handleBlur}
        value={formik.values.lastName}
      />
      {formik.touched.lastName && formik.errors.lastName ? (
        <div>{formik.errors.lastName}</div>
      ) : null}

      <label htmlFor="email">Email Address</label>
      <input
        id="email"
        name="email"
        type="email"
        onChange={formik.handleChange}
        onBlur={formik.handleBlur}
        value={formik.values.email}
      />
      {formik.touched.email && formik.errors.email ? (
        <div>{formik.errors.email}</div>
      ) : null}

      <button type="submit">Submit</button>
    </form>
  );
};
```
### Part 3: getFieldProps()
```
import React from "react";
import { useFormik } from "formik";
import * as Yup from "yup";

export const SignupForm = () => {
  // Pass the useFormik() hook initial form values and a submit function that will
  // be called when the form is submitted
  const formik = useFormik({
    initialValues: {
      firstName: "",
      lastName: "",
      email: "",
    },
    validationSchema : Yup.object({
      //validiation logic written using Yup methods
      firstName: Yup.string()
        .max(15, 'Must be 15 characters or less')
        .required('Required'),
      lastName: Yup.string()
        .max(20, 'Must be 20 characters or less')
        .required('Required'),
      email: Yup.string().email('Invalid email address').required('Required'),
    }),
    onSubmit: (values) => {
      alert(JSON.stringify(values, null, 2));
    },
  });
  return (
    <form onSubmit={formik.handleSubmit}>
      <label htmlFor="firstName">First Name</label>
      <input
        id="firstName"
        name="firstName"
        type="text"
        //some field-level info, it returns to you the exact group of onChange, onBlur, value, checked for a given field.
        // You can then spread that on an input, select, or textarea.
        {...formik.getFieldProps('firstName')}
      />
      
      {//with touched, formik tracks which fields have been visited
      formik.touched.firstName && formik.errors.firstName ? (
        <div>{formik.errors.firstName}</div>
      ) : null}

      <label htmlFor="lastName">Last Name</label>
      <input
        id="lastName"
        name="lastName"
        type="text"
       //some field-level info, it returns to you the exact group of onChange, onBlur, value, checked for a given field.
        // You can then spread that on an input, select, or textarea.
        {...formik.getFieldProps('lastName')}
      />
      {formik.touched.lastName && formik.errors.lastName ? (
        <div>{formik.errors.lastName}</div>
      ) : null}

      <label htmlFor="email">Email Address</label>
      <input
        id="email"
        name="email"
        type="email"
        //some field-level info, it returns to you the exact group of onChange, onBlur, value, checked for a given field.
        // You can then spread that on an input, select, or textarea.
        {...formik.getFieldProps('email')}
      />
      {formik.touched.email && formik.errors.email ? (
        <div>{formik.errors.email}</div>
      ) : null}

      <button type="submit">Submit</button>
    </form>
  );
};

```
### Part 4: <Formik>
import React from "react";
import { Formik } from "formik";
import * as Yup from "yup";

export const SignupForm = () => {
 //The <Formik> component accepts a function as its children (a.k.a. a render prop).
 // Its argument is the exact same object returned by useFormik()
  return (
    <Formik
    initialValues={{ firstName: '', lastName: '', email: '' }}
    validationSchema={Yup.object({
      firstName: Yup.string()
        .max(15, 'Must be 15 characters or less')
        .required('Required'),
      lastName: Yup.string()
        .max(20, 'Must be 20 characters or less')
        .required('Required'),
      email: Yup.string().email('Invalid email address').required('Required'),
    })}
    onSubmit={(values, { setSubmitting }) => {
      setTimeout(() => {
        alert(JSON.stringify(values, null, 2));
        setSubmitting(false);
      }, 400);
    }}
  >
    {formik => (<form onSubmit={formik.handleSubmit}>
      <label htmlFor="firstName">First Name</label>
      <input
        id="firstName"
        name="firstName"
        type="text"
        //some field-level info, it returns to you the exact group of onChange, onBlur, value, checked for a given field.
        // You can then spread that on an input, select, or textarea.
        {...formik.getFieldProps('firstName')}
      />
      
      {//with touched, formik tracks which fields have been visited
      formik.touched.firstName && formik.errors.firstName ? (
        <div>{formik.errors.firstName}</div>
      ) : null}

      <label htmlFor="lastName">Last Name</label>
      <input
        id="lastName"
        name="lastName"
        type="text"
       //some field-level info, it returns to you the exact group of onChange, onBlur, value, checked for a given field.
        // You can then spread that on an input, select, or textarea.
        {...formik.getFieldProps('lastName')}
      />
      {formik.touched.lastName && formik.errors.lastName ? (
        <div>{formik.errors.lastName}</div>
      ) : null}

      <label htmlFor="email">Email Address</label>
      <input
        id="email"
        name="email"
        type="email"
        //some field-level info, it returns to you the exact group of onChange, onBlur, value, checked for a given field.
        // You can then spread that on an input, select, or textarea.
        {...formik.getFieldProps('email')}
      />
      {formik.touched.email && formik.errors.email ? (
        <div>{formik.errors.email}</div>
      ) : null}

      <button type="submit">Submit</button>
    </form>)
}
</Formik>
  )
};

## How to split UI components
1. Each component should be a logical separation of content or logical division of the layout.
2. Each component should be reusable within the app as much as possible. Howvever, not all components are meant to be reuasble
3. Each component shpould a single, well defined responsibility.
4. No too many states or props in a single component
5. Name a component according to what it does or what it displays.
6. Colocate related components in the same file.
