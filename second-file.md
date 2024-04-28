Idea is to rubber duck every line of code in Traversy media playlist. Leggo!

![crud mapping to http requests and responses](https://networkop.co.uk/img/rest-crud.png)

1. `npm init`: It is a command used in the world of Node.js development to initialize a new project. It creates a file called `package.json` at the root of your project directory. This file acts like a blueprint for your project, storing important information such as:

* Project name
* Project version
* Project description
* Dependencies (other code libraries your project relies on)
* Scripts (automated tasks you can run with npm commands)
* License

There are two main ways to use `npm init`:
a. **Interactive mode (default):** When you run `npm init` in your terminal, it will prompt you with a series of questions about your project. You can answer these questions to provide the information needed for the `package.json` file.

b. **Non-interactive mode (with `-y` flag):** If you want to skip the questions and use defaults, you can use the `-y` (or `--yes`) flag along with the command, i.e. `npm init -y` This will create a `package.json` file with basic defaults.
   
2. `.gitignore`: It's a text file that tells **Git** which files and folders to ignore, essentially keeping them out of your version control history.

Here's how it works:
* You create a file named `.gitignore` (the dot is important) at the root of your Git repository.
* Each line in the `.gitignore` file specifies a pattern that matches files or folders Git should ignore.
* Git checks the patterns in the `.gitignore` file whenever you add, commit, or push changes.

There are different types of patterns you can use in a `.gitignore` file, but some common ones include:
*  **Filename:** To ignore a specific file, you simply list its name (e.g., `readme.txt`).
*  **Wildcard:** You can use an asterisk (*) to match any characters in a filename (e.g., `*.log` to ignore all log files).
*  **Directory:** To ignore an entire directory, list its name followed by a forward slash (e.g., `/build`).
*  **Glob patterns:** These allow for more complex matching using special characters like question mark (?) for single character match or brackets [] for a range of characters.

By using a `.gitignore` file, you can keep your version control history clean and free of unnecessary files, such as:
*  **Temporary files:** Files created by your development environment that aren't part of your actual code.
*  **Compiled files:** Files generated from your source code during the build process.
*  **Configuration files:** Files specific to your development machine or environment.
*  **Third-party libraries:** If you're using pre-built libraries from npm or similar package managers, you typically don't want to track them in your Git repository.

Here are some additional points to keep in mind about `.gitignore` files:
* The `.gitignore` file itself is tracked by Git.
* You can have multiple `.gitignore` files within your repository for more granular control.
* There are also global ignore rules you can configure to apply to all your Git repositories.
* Several online resources provide pre-made `.gitignore` templates for different programming languages and frameworks, which can save you time when setting up a new project.

3. The command `npm i -D nodemon` is used to install the `nodemon` package as a development dependency in a Node.js project.

Here's a breakdown of the command:
* `npm`: Stands for Node Package Manager, the tool used to install and manage JavaScript packages for Node.js projects.
* `i`: Short for `install`, the command to install packages from the npm registry.
* `-D`: Stands for `--save-dev`, which indicates that the package should be installed as a development dependency. This means the package will be included in the project's `package.json` file under the `devDependencies` section, but it won't be bundled with the production code. Development dependencies are typically tools or libraries used during development but not required for running the application in its deployed state.
* `nodemon`: The name of the package you want to install. In this case, it's `nodemon`, a popular tool for watching Node.js files for changes and automatically restarting the server when changes are detected. This can save developers a lot of time and effort during the development process.

So, in essence, `npm i -D nodemon` installs the `nodemon` package as a development dependency for your Node.js project, making it available for use during development but not included in the production code.

Here's an example of how to use `npm i -D nodemon` in your terminal:
```
npm i -D nodemon
```

This will install the `nodemon` package and add it to your project's `package.json` file under the `devDependencies` section. Once installed, you can use `nodemon` to watch your Node.js files for changes and automatically restart the server when changes are detected. For example, to run your Node.js application using `nodemon`, you would use the following command:
```
nodemon your-script.js
```
Replace `your-script.js` with the actual filename of your Node.js script. `nodemon` will then watch `your-script.js` and any other files in the current directory for changes. If it detects any changes, it will automatically restart the server, saving you the hassle of manually restarting the server after each code change.

4. **dotenv**:It's a lightweight Node.js package that helps you load environment variables from a `.env` file into the `process.env` object. Environment variables are key-value pairs that store configuration settings or sensitive information like API keys or database passwords.

**Why use dotenv?**
* **Separation of Concerns:** It keeps your environment variables separate from your code, making your code cleaner and more secure. You don't commit your `.env` file to version control, so sensitive information isn't accidentally exposed.
* **Flexibility:** You can easily manage different environments (development, testing, production) by having separate `.env` files for each.
* **Convenience:** It simplifies managing environment variables, especially when working on a project with multiple developers.

**How to use dotenv:**
a. **Install dotenv:**
   ```bash
   npm install dotenv
   ```

b. **Create a `.env` file:**
   - Create a file named `.env` at the root of your project directory.
   - Inside the `.env` file, define your environment variables like this:
     ```
     DB_HOST=localhost
     DB_USER=my_username
     DB_PASSWORD=my_password
     ```

c. **Use dotenv in your code:**
   ```javascript
   require('dotenv').config();

   console.log(process.env.DB_HOST); // Outputs: localhost
   ```
By calling `require('dotenv').config()`, you tell dotenv to load the environment variables from the `.env` file into the `process.env` object. Then, you can access these variables throughout your code using `process.env`.

**Additional Points:**
* Dotenv doesn't modify the actual `process.env` object. It creates a copy and adds the loaded variables to that copy.
* Refer to the dotenv documentation for more details [https://www.npmjs.com/package/dotenv](https://www.npmjs.com/package/dotenv).
***

5. The command `git init` is used to create a new Git repository.  Here's a breakdown of what it does:

* **Creates a hidden directory:** When you run `git init` in your project directory, it creates a hidden directory called `.git`. This directory stores all the information about your Git repository, including things like version history, branches, and tracked files.
* **Initializes an empty repository:** By default, `git init` creates an empty repository with no commits yet. It sets up the basic structure for tracking changes to your project files.
* **Creates a default branch (optional):** Typically, `git init` also creates a default branch, often named `main` (or sometimes `master` in older setups). This branch acts as a pointer to the current state of your project.

6. `const dotenv = require("dotenv").config()`: is used to load environment variables from a `.env` file into your Node.js application using the `dotenv` package. Let's break it down:

a. **`const dotenv = ...`**:
   - This line declares a constant variable named `dotenv`.
   - The `const` keyword ensures the value assigned to `dotenv` cannot be changed later in your code.

b. **`require("dotenv")`**:
   - This part uses the `require` function, a core functionality in Node.js for importing modules.
   - It's saying, "I need the functionality provided by the `dotenv` module."

c. **`.config()`**:
   - This calls the `config` function from the `dotenv` module after it's imported.
   - The `.config()` function is responsible for:
     - Reading the `.env` file (by default, located in the root of your project directory).
     - Parsing the key-value pairs defined in the `.env` file.
     - Adding those key-value pairs as properties to the `process.env` object in your Node.js environment.

**In essence:**

This single line of code sets up dotenv to load environment variables from a `.env` file and make them accessible throughout your application using the `process.env` object.

**Example `.env` file:**
```
DB_HOST=localhost
DB_USER=my_username
DB_PASSWORD=my_password
```

**Accessing environment variables:**
After the dotenv configuration, you can access the loaded variables like this:

```javascript
console.log(process.env.DB_HOST); // Outputs: localhost (assuming that's what's set in your .env file)
```
7. 
