# Part F: GET data from the Kintone App

Let's grab data from the Kintone Database App and output it to our frontend React App!

To implement the GET request, we will be editing the following two files:
  * [backend - server.js](#backend---serverjs)
  * [frontend - index.js](#frontend---indexjs)

---

## backend - server.js
We will set up an Express server that calls Kintone on behalf of the frontend React App to avoid the CORS error.

Expected result:
  * Calls Kintone's GET Records API when <http://localhost:5000/getData> endpoint is requested with a GET request
  * Returns the JSON response to frontend React App (<http://localhost:3000>)

File Location: `.../myproject/backend`

```js
// Express Server Setup
const express = require('express');
const cors = require('cors');
const fetch = require('node-fetch');

const PORT = 5000;
const app = express();

// Parse incoming requests with JSON payloads
app.use(express.json());

// Set Cross-Origin Resource Sharing (CORS) to frontend React App
app.use(cors());
const corsOptions = {
  origin: "http://localhost:3000"
};

// Kintone API Setup
const subdomain = ""; //Enter your Kintone Subdomain (ex: devevents)
const appID = ""; //Enter your App's ID number (ex: 1)
const apiToken = ""; //Enter your App's API Token (ex: cJrAD9...)

// Append a Query Parameters to the Request Endpoint
const parameters = "query=order by recordID asc";

const multipleRecordsEndpoint = `https://${subdomain}.kintone.com/k/v1/records.json?app=${appID}&${parameters}`

// This runs if a GET request calls for localhost:5000/getData
app.get('/getData', cors(corsOptions), async (req, res) => {
  const fetchOptions = {
    method: 'GET',
    headers: {
      'X-Cybozu-API-Token': apiToken
    }
  }
  const response = await fetch(multipleRecordsEndpoint, fetchOptions);
  const jsonResponse = await response.json();
  res.json(jsonResponse);
});

app.listen(PORT, () => {
  console.log(`Example app listening at http://localhost:${PORT}`);
});
```

---

## frontend - index.js
Now that we got our Express server setup, time for configuring the frontend React App!  

Expected Result:  
Data from the Kintone App will be outputted as bullet points at <http://localhost:3000/>.

File Location: `.../myproject/frontend/src/index.js`

```jsx
import React, { useState, useEffect } from 'react';
import ReactDOM from 'react-dom';

// Declare the GET endpoint defined in our Express server
const getRecordsEndpoint = "http://localhost:5000/getData";

const callRestApi = async () => {
  const response = await fetch(getRecordsEndpoint);
  const jsonResponse = await response.json();

  console.log(jsonResponse);

  // return JSON.stringify(jsonResponse);

  // Create an array of lists by looping through Kintone's responded array

  //record.title.value = value of the Title field
  //record.author.value = value of the author field

  // In React, assign a unique ID to each created list
  // Use record.recordID.value for key
  const arrayOfLists = jsonResponse.records.map(
    record => <li key={record.recordID.value}><b>{record.title.value}</b> written by {record.author.value}</li>
  )
  return arrayOfLists;
};

function RenderResult() {
  const [apiResponse, setApiResponse] = useState("*** now loading ***");

  useEffect(() => {
    callRestApi().then(
      result => setApiResponse(result));
  }, []);

  return (
    <div>
      <h1>React App</h1>
      <ul>{apiResponse}</ul>
    </div>
  );
};

ReactDOM.render(
  <RenderResult />,
  document.querySelector('#root')
);
```

---

## Result - Kintone Database App's data displayed as bullet points

Here is what it looks like when displaying our Manga DB App.  
It lists out our favorite Japanese comics, ordered by `recordID`.

![Will's Article - React App with Clean Kintone Data](https://res.cloudinary.com/practicaldev/image/fetch/s--mL-QZl81--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4qj4lm74w34y3kct44px.png)
