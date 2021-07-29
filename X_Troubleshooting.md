# Troubleshooting Notes

## Starting the frontend React Project
Enter the following commands in your terminal
  * $ `cd ../myproject/frontend`
  * $ `npm start`

Then access your React project at
  * `http://localhost:3000/`

## Starting the backend Express Server
Enter the following commands in your terminal
  * $ `cd ../myproject/backend`
  * $ `node server.js`

Then access your Express server at
  * `http://localhost:5000/`

Access the Kintone API call at
  * `http://localhost:5000/getData`

## Kintone Section: React not updating after updating server.js
Be sure to restart the server after making changes to server.js!  

(1) Go to the terminal running the Express server.
    It should look something like this:

  ```shell
  user@computer backend % node server.js
  Example app listening at http://localhost:${PORT}
  ```

(2) Restart the Express server
  * Stop the server: `ctrl + c`
  * Start the server: $ `node server.js`

(3) Reload the browser showing the React App.
  * `http://localhost:3000/`

## Kintone API Token

To generate an API Token for a Kintone App:
1. Go to the Kintone App
2. Go to the Gear icon ⚙️ (top right corner) > Open the App Settings page
3. Click on the **App Settings** Tab > Click on **API Token** settings
4. Click the `Generate` button to generate a token
5. Click the `Save` button (top left corner) to save the token setting
6. Finally, click the `Update App` button (top right corner) to implement the token setting change.

![Generating an API Token Gif](https://user-images.githubusercontent.com/30670749/111570449-3964c580-87e8-11eb-83ee-9a6a1ff2e8df.gif)
