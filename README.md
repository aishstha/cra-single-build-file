# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.
## steps to build single bundle file :

### step 1 : npm run eject

### step 2 : go to the config/webpack.config.js

check this differences (https://www.diffchecker.com/7a1Hdg3a). you have to make this diff in your webpack.config.js file (same as in the left section).

### step 3 : create server.js file in root folder and keep this code inside it.
```
const express = require("express");
const morgan = require("morgan");
const openBrowser = require("react-dev-utils/openBrowser");

const app = express();
const currentDirectory = process.cwd();
const { HOST, PORT } = process.env;

app.use(morgan("tiny")); // XHR request logging framework
app.use(express.static("build")); // express will serve up production assets
app.get("*", (req, res) =>
  res.sendFile(`${currentDirectory}/build/index.html`)
); // express will serve up the front-end index.html file if it doesn't recognize the route

app.listen(PORT, err => {
  if (!err) {
    const url = `${HOST}${PORT}`;
    console.log(`\nYour application is running on \x1b[1m${url}\x1b[0m\n`);
    openBrowser(url);
  } else {
    console.err(`\nUnable to start server: ${err}`);
  }
});
```

### step 4 : npm run build 
or 
### step 4 : keep "analyze": "analyzeChunks=true node scripts/build.js" inside scripts in package.json and do npm run analyze

Builds the app to the `build` folder.\

The build(build/static/js/bundle.min.js) is minified and the filenames include the hashes.\
Your app is ready to be deployed!

For more information follow https://stackoverflow.com/a/59332075
