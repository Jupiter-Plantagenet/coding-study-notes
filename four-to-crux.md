
What is a Middleware?
A middleware is a function that takes in an HTTP request and response object, plus the next middleware function in the chain.
The function can look at and modify the request and response objects, respond to requests, or decide tocontinue with middleware chain by calling the next middleware function.

What does `express.static()` do?
The built-in express.static function generates a middleware function that responds to a request by trying to match the request URL with a file under a directory specified
by the argument to the static function. If a file exists, it returns the contents of the file as the response, ifnot, it chains to the next middleware function. 

How do you mount a middle ware to an express app?
This is done with the `use()` of the app. The first argument to this method is the base URL of any HTTP request to match. The second argument is the middleware function itself.

How do you specify the entry point for an express server to node?
In Scripts section of package.json, write;
`"start": "node server/server.js"`
if the entry file is called server.js and located in a folder called server that is it self in the root directory

How to setup Babel automated transpilation and Nodemon at buildtime
1. Run the follwoing commands:
   `npm install --save-dev @babel/core@7 @babel/cli@7` to install babel core library and cli
   `npm install --save-dev @babel/preset-react@7` for the babel JSX transform preset
2. In scripts section of package.json, write:
   `"start": "nodemon -w server server/server.js"`: Watch server directoru for any change in files and run server/server.js
   `"compile": "babel src --out-dir public"`: Compile jsx in src directory into js in public directory(js file auto-generated)
   `"watch": "babel src --out-dir public --watch --verbose"`: Wach for changes in src directory and print out a line in console upon any change

(https://www.youtube.com/watch?v=l8WPWK9mS5M&t=241s) Build Rest API

(https://webdesign.tutsplus.com/build-a-simple-weather-app-with-vanilla-javascript--cms-33893t) Build Simple Weather app

(https://www.taniarascia.com/crud-app-in-react-with-hooks/) Simple Crud App

(https://www.youtube.com/watch?v=SjjmHNdE32Y) Minimialist Portfolio Website
