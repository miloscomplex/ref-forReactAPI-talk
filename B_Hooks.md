# Part B: Using Hooks in React!

We will use `useState` & `useEffect` Hooks to handle the REST API calls in React.

---

## What is `useState` & `useEffect` Hooks

[useState hooks](https://reactjs.org/docs/hooks-state.html) allow us to use special "state" variables that we can utilize to render into the React UI.

[useEffect hooks](https://reactjs.org/docs/hooks-effect.html) allow us to run functions after the rendering has finished. We'll use this to run a REST API call and update the state variable, which will then cause React to re-render the UI.

## Sample Code for index.js

File Location: `.../myproject/frontend/src/index.js`

```jsx
// Get started by importing the React JavaScript library & Hooks
import React, { useState, useEffect } from 'react';
import ReactDOM from 'react-dom';

// Call Random User Generator API
const restEndpoint = "https://randomuser.me/api/";

// Wait for response & return the API response
const callRestApi = async () => {
  const response = await fetch(restEndpoint);
  const jsonResponse = await response.json();

  console.log(jsonResponse);

  return JSON.stringify(jsonResponse);
};

const RenderResult = () => {
  // Establish useState by giving it our initial state
  // const [state, setState] = useState(initialState);
  const [apiResponse, setApiResponse] = useState("*** now loading ***");

  // useEffect takes 2 arguments:
  // 1st = a function, called effect, that is executed when the React Component is rendered
  // 2nd = Array of dependencies to control when effect is to be executed after mounting the component; Empty array = only invoke effect once

  useEffect(() => {
    callRestApi().then(
      result => setApiResponse(result));
  }, []);

  return (
    // JSX includes html-like syntax
    <div>
      <h1>React App</h1>
      <p>{apiResponse}</p>
    </div>
  );
};

// Where the magic happens!
ReactDOM.render(
  <RenderResult />,
  document.getElementById('root')
);
```

---

## Result - Success

Expected output:  
Outputs the Random User API Call to the frontend React App.

![React App with Random User API - Will's Article](https://res.cloudinary.com/practicaldev/image/fetch/s--gLC8WZiw--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/s4hy00cysrqc0a8n2jkf.gif)
