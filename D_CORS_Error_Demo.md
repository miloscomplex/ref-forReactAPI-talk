# Part D: CORS Error Demo

Now that we are outputting Random User Generator API's response onto our frontend React App let's output more useful results!  
Using Kintone's low-code Database platform, we can easily create & host a database that is accessible with REST APIs.

But can we just swap the request endpoint with Kintone's?

---

## Sample Code for index.js
We will try a GET request to Kintone from our frontend React App.

If you want to run this code, be sure to input your Kintone specifications for `subdomain`, `appID`, and `apiToken`.

File Location: `.../myproject/frontend/src/index.js`

```jsx
import React, { useState, useEffect } from 'react';
import ReactDOM from 'react-dom';

// Kintone API Setup
const subdomain = ""; //Enter your Kintone Subdomain (ex: devevents)
const appID = ""; //Enter your App's ID number (ex: 1)
const apiToken = ""; //Enter your App's API Token

const getKintoneData = async () => {
  const requestEndpoint = `https://${subdomain}.kintone.com/k/v1/records.json?app=${appID}`;
  const fetchOptions = {
    method: 'GET',
    headers: { 'X-Cybozu-API-Token': apiToken }
  };
  const response = await fetch(requestEndpoint, fetchOptions);
  const jsonResponse = await response.json();
  console.log(jsonResponse);
  return JSON.stringify(jsonResponse);
};

const RenderResult = () => {
  const [apiResponse, setApiResponse] = useState("*** now loading ***");

  useEffect(() => {
    getKintoneData().then(
      result => setApiResponse(result));
  }, []);

  return (
    <div>
      <h1>React App</h1>
      <p>{apiResponse}</p>
    </div>
  );
};

ReactDOM.render(
  <RenderResult />,
  document.getElementById('root')
);
```

---

## Result - CORS Error

[Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) Error occurs since we cannot access the resources that lie on Kintone's domain directly from our domain (frontend React App).

![CORS_Error_Crop.png Kintone_React_Workshop v2.1](https://user-images.githubusercontent.com/30670749/125892916-ef0f189c-af9f-4dc4-95d6-c0a111bb7238.png)
