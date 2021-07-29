# Part A: Using Promises in React

When getting data from an API call, we usually need to use [promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises), right?  
So let's try that in our frontend React App.

---

## Sample Code for index.js
Here is an example that tries to output an API response in the frontend React App.  
It calls [Random User Generator API](https://randomuser.me/api/), waits for a response, and then creates a React element using the JSON data.  
Let's see what happens!  

File Location: `.../myproject/frontend/src/index.js`

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

// Call Random User Generator API
const restEndpoint = 'https://randomuser.me/api/';

// Wait for response & tries to output it to React
const callRestApi = async () => {
  const response = await fetch(restEndpoint);
  const jsonResponse = await response.json();
  console.log(jsonResponse);

  // React.createElement( type, [properties], [...children]);
  return React.createElement('h1', null, JSON.stringify(jsonResponse));
};

ReactDOM.render(
  callRestApi(),
  document.querySelector('#root')
);
```

---

## Result - Error

The `callRestApi()` async function returns a promise object immediately as it waits for the Random User Generator API's response.  
React doesn't "wait" for the REST API result, so it tries to create and render the element with the promise object immediately and failing.
It attempts to display the Random User Generator API response into a React element.  
However, the following error will display instead:

```text
Error: Objects are not valid as a React child (found: [object Promise]). If you meant to render a collection of children, use an array instead.
```

![Promise_Error.png - Kintone_React_Workshop - v2.1](https://user-images.githubusercontent.com/30670749/125893011-dbc39697-4944-4684-84a7-1472aeeb8407.png)
