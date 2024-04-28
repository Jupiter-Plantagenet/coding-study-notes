#Concepts Only!

To build a fullsatck app, you need a directory with two sub directories: Client and Server. Below is the setup:

###Client
1. Create a vite app with a react template: `npm create vite@latest` and follow the prompt to create the clientside react app.
2. Run `npm install axios moment react-file-base64 redux redux-thunk`
   - axios: handles http requests
   - moment: simplifies working with time and date
   - react-file-base64: converts images
   - redux: working with state using reducers
   - redux-thunk: asynchronous operations with redux


 ###Server
 1. Run `npm init` to create *package.json* and specify the entry point of the serverside app. Let's assume it is called *index.js*
 2. In *package.josn* specify the following
    ```
      //Allows use of import/export syntax
      "type": "module",
      // makes npm start run nodemon on the entry point of the sever side app
      "scripts":{
            "start" : "nodemon index.js"
    ```
 3. run 'npm install body-parser cors express mongoose nodemon`.
   - body-parser: enables us to send POST requests
   - cors: allows us to send cross-origin requests
   - express: for developing the serverside functionalities
   - mongoose: for creating models for our data
   - nodemon: for hot reloading

`bodyParser.json({"100mb", extended: true})` sets the maximum size of the request body to 100mb and parses the URL-encoded data with the qs library (when true).
 
