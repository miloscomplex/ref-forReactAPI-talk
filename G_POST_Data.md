# Part G: POST data to the Kintone App

Now that we can retrieve & display the data from the Kintone Database App let's submit new data via our frontend React App!  
We will do this by adding a POST request route on the Express server used when the user inputs via the form on the frontend React App.

To implement the POST request, we will be editing the following two files:
  * [backend - server.js](#backend---serverjs)
  * [frontend - index.js](#frontend---indexjs)

**Note**  
Be sure to restart your Express server when updating `server.js`.
  * `Control` + `C` to end the Express server
  * `node server.js` to start it up again

## backend - server.js
We will add another endpoint to make our POST requests.

Expected result:
  * When `localhost:5000/getData` endpoint is called, a GET request is sent to Kintone for data retrieval.
  * When `localhost:5000/postData` endpoint is called, a POST request is sent to Kintone to update the database with the submitted entry.

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

// Call Kintone's GET Records API
const multipleRecordsEndpoint = `https://${subdomain}.kintone.com/k/v1/records.json?app=${appID}&${parameters}`

// Call Kintone's GET Record API
const singleRecordEndpoint = `https://${subdomain}.kintone.com/k/v1/record.json?app=${appID}&${parameters}`;

// This runs if a GET request calls for localhost:5000/getData
app.get('/getData', cors(corsOptions), async (req, res) => {
  const fetchOptions = {
    method: 'GET',
    headers: {
      'X-Cybozu-API-Token': apiToken
    }
  }
  // const response = await fetch(requestEndpoint, fetchOptions);
  const response = await fetch(multipleRecordsEndpoint, fetchOptions);

  const jsonResponse = await response.json();
  res.json(jsonResponse);
});

// Add a New Route for a POST request using singleRecordEndpoint

// This runs if a POST request calls for localhost:5000/postData
app.post('/postData', cors(corsOptions), async (req, res) => {
  const requestBody = {
    "app": appID,
    "record": {
      "title": {
        "value": req.body.title
      },
      "author": {
        "value": req.body.author
      }
    }
  };
  const options = {
    method: 'POST',
    headers: {
      'X-Cybozu-API-Token': apiToken,
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(requestBody)
  }
  const response = await fetch(singleRecordEndpoint, options);
  const jsonResponse = await response.json();
  res.json(jsonResponse);
});

app.listen(PORT, () => {
  console.log(`Example app listening at http://localhost:${PORT}`);
});
```

## frontend - index.js
We will add a form for user input and function to make a POST request on our newly defined Express server's endpoint.


Expected result:
  * Display Kintone app data as a clean list
  * Form at the bottom to add user input
  * When an input is submitted, a POST request is sent out & the list is updated

File Location: `.../myproject/frontend/src/index.js`

```jsx
import React, { useState, useEffect } from 'react';
import ReactDOM from 'react-dom';

// Declare the GET & POST endpoints defined in our Express server
const getRecordsEndpoint = "http://localhost:5000/getData";
const addRecordEndpoint = "http://localhost:5000/postData";

const callRestApi = async () => {
  const response = await fetch(getRecordsEndpoint); //Update endpoint
  const jsonResponse = await response.json();
  console.log(jsonResponse);
  const arrayOfLists = jsonResponse.records.map(
    record => <li key={record.recordID.value}><b>{record.title.value}</b> written by {record.author.value}</li>
  )
  return arrayOfLists;
};

// Make REST API Calls & take in the values stored in the state variables related to the input fields
const AddNewRecord = async (Title, Author) => {
  const RecordBodyParameters = {
    'title': Title,
    'author': Author
  }

  const options = {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(RecordBodyParameters)
  }

  const response = await fetch(addRecordEndpoint, options);
  const jsonResponse = await response.json();
  console.log(JSON.stringify(jsonResponse));
  return jsonResponse;
};

function RenderResult() {
  const [apiResponse, setApiResponse] = useState("*** now loading ***");

  // Create States for the Input Fields
  const [titleValue, setTitleValue] = useState("");
  const [authorValue, setAuthorValue] = useState("");
  const [successCounter, setSuccessCounter] = useState(0);

  useEffect(() => {
    callRestApi().then(
      result => setApiResponse(result));
  }, [successCounter]);

  // Define the onChange functions
  function HandleTitleChange(event) {
    setTitleValue(event.target.value);
  }

  function HandleAuthorChange(event) {
    setAuthorValue(event.target.value);
  }

  // Define the Button Click function
  function ButtonClick() {
    setApiResponse(apiResponse.concat(<li key="0" >*** now loading ***</li>));
    AddNewRecord(titleValue, authorValue)
      .then(response => {
        setSuccessCounter(successCounter + 1);
      });
  }

  // Append a form for user input
  return (
    <div>
      <h1>React App</h1>
      <ul>{apiResponse}</ul>
      <form>
        <div>
          <label htmlFor="title-input">Title:</label>
          <input type="text" value={titleValue} id="title-input" onChange={HandleTitleChange} />
        </div>
        <div>
          <label htmlFor="author-input">Author:</label>
          <input type="text" value={authorValue} id="author-input" onChange={HandleAuthorChange} />
        </div>
        <button type="button" onClick={ButtonClick}>Add data</button>
      </form>
    </div>
  );
};

ReactDOM.render(
  <RenderResult />,
  document.querySelector('#root')
);
```

## Result - Kintone Database App's data displayed as bullet points with a form to submit a new entry

![Will's Article - React App with Data & Form](https://res.cloudinary.com/practicaldev/image/fetch/s--IwgycySX--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/a8ls55md2dhqm82ksspe.png)
