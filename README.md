﻿# reactapp-node

This project has been built on node.js with Express with react js as frontend and deploy it on heroku.

## Tools You Will Need:

- Make sure Node and NPM are installed on your computer. You can download both at nodejs.org (NPM is included in your Node installation)
- Use a code editor of your choice. I am using and would personally recommend using VSCode. You can download VSCode at code.visualstudio.com.
- Make sure you have Git installed on your computer. This is necessary for deploying our application with Heroku. You can get it at git-scm.com
- An account at heroku.com. We will use Heroku to publish our app to the web entirely for free.

## Initial Setup:

- Install requirements

```
$ npm install
```

## Run server:

Using the following command will run the server in `http://localhost:3001/`.

```
$ npm run start
```

The frontend application connects to this namespaces`http://localhost:3000/`.

## To start web server add below text in server/package.json

```
"scripts": {
  "start": "node server/index.js"
},
```

## - Create an API Endpoint in server/index.js (add below code)

```
app.get("/api", (req, res) => {
  res.json({ message: "Hello from server!" });
});

app.listen(PORT, () => {
  console.log(`Server listening on ${PORT}`);
});
```

### To test npm start:

```
http://localhost:3001/api
```

## Create your React frontend

```
npx create-react-app client
```

### add a property called proxy in client/package.json

```
"proxy": "http://localhost:3001",
```

### start up our React app

### make sure to cd into the newly-created client folder then

```
cd client
npm start
```

## Make HTTP Requests from React to Node

### in file client/src/App.js

```
import React from "react";
import logo from "./logo.svg";
import "./App.css";

function App() {
  const [data, setData] = React.useState(null);

  React.useEffect(() => {
    fetch("/api")
      .then((res) => res.json())
      .then((data) => setData(data.message));
  }, []);

  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>{!data ? "Loading..." : data}</p>
      </header>
    </div>
  );
}

export default App;
```

## Deploy your app to the web with Heroku

### get back to root folder

```
cd client
rm -rf .git
```

### add code in server/index.js

```
const path = require('path');
const express = require('express');

...

// Have Node serve the files for our built React app
app.use(express.static(path.resolve(__dirname, '../client/build')));

// Handle GET requests to /api route
app.get("/api", (req, res) => {
  res.json({ message: "Hello from server!" });
});

// All other GET requests not handled before will return our React app
app.get('*', (req, res) => {
  res.sendFile(path.resolve(__dirname, '../client/build', 'index.html'));
});
```

### Build our React app for production- add in server/package.json

```
"scripts": {
    "start": "node server/index.js",
    "build": "cd client && npm install && npm run build"
  },
```

### add engine field in server/package.json

```
"engines": {
  "node": "your-node-version"
}
```

- Create your account in heroku app and create project

### Install CLI

```
sudo npm i -g heroku
```

### Log in to Heroku through the CLI

```
heroku login

Press any key to login to Heroku
```

### Deploy

```
git init
heroku git:remote -a insert-your-app-name-here
git add .
git commit -am "Deploy app to Heroku"
```

```
git push heroku main
```

## Full-stack React and Node app is LIVE now.

### Show your support

Give a ⭐ if you like this!

<a href="https://www.buymeacoffee.com/sandeepmaharjan" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-violet.png" alt="Buy Me A Coffee" height= "60px" width= "217px" ></a>
