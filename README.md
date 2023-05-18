# ExpressUserIntro

## Overview

- Create a simple express server capable of performing non-persisted CRUD (Create, Read, Update, Delete) operations.
- The server should be capable of creating a new user via POST request
- The server should be capable of responding with the entire list of users
- The Server should be capable of responding with a single user that has been looked up via phone number
- The server should be capable of responding with several users that has been looked up via country
- The server should be capable of updating a user with new user data, use email to find the user
- The server should be capable of deleting a user that has been looked up via cell number

## Instructions

### 1) Project Setup

- Go to github and create a new github repo
- In the Create a new repository screen, set the following options
  - Set Repository template to No template
  - Set the owner to yourself and the repository name as ExpressUserIntro
  - Leave the description blank
  - Set the repository to public
  - Leave Add a README file unchecked
  - Set the Add .gitignore template option to Node
  - Leave the Choose a license as None
- Click the Create repository button
- ## In the repository screen, click the green <> Code dropdown button, copy the url that shows under the Local -> Clone -> HTTPS tab. It should look something like
  ```
  https://github.com/your-git-username/ExpressUserIntro.git
  ```
- ## Open a new terminal window on your computer, cd into the folder where you keep your CodeImmersives repositories and clone the ExpressUserIntro repository to your local file system with the following command:
  ```
  git clone <your github repository>
  ```
- cd into the ExpressUserIntro folder
- ## Initialize the folder as an npm project with the following command
  ```
  npm init -y
  ```
  - _Commentary_: This command will create a package.json file in your repository. The package.json is a special file used by npm to track meta info about your project such as what libraries you have installed, the project name, start scripts you have defined, etc. The -y flag will skip the initial prompt of defining some of your project fields such as project name, version, etc.
- ## Install the express and nodemon npm packages with the following command
  ```
  npm install express
    npm install --save-dev nodemon
  ```
  - _Commentary_:
    - If you look inside your package.json file now, you should see express listed as a dependencies and nodemon as devDependencies. A project dependency is a package/library that is required for your application to run. When you install a package, all the code for that package is downloaded into the node_modules folder in your project.
    - Node_modules tend to be very large folders/files. In web development, teams of developers will collaborate by downloading each others repository code. If every developer had to download all the node_modules every time they cloned a repository, it would take a lot of time and network bandwith to do so.
    - So in order to avoid this problem, we ignore the node*modules folder via the .gitignore file. Open the .gitignore file in your repository and skim through it. Every filename listed here will be ignored by git when you make a commit. If you see the '*' symbol, that stands for wildcard and will match any name. \_.log for instance will ignore all files that end in .log.
    - Note how in the .gitignore file node_modules is listed. Thus, when you commit your code to github, the node_modules folder and all subfolders inside of it will be ignored. So when dev teams download each others repositories, there will be no node_modules folder. The first step that developers will do when downloading a new repository is to run the 'npm install' command. This command will look at all the dependencies listed in the package.json file and download the corresponding npm package into your local file system. This pattern allows developers to add npm packages to their projects without needing to send the files through github.
- Create a new file called app.js in your ExpressUserIntro folder.
  - ## _Optional_: The terminal command for creating a new file is touch {file-name}. So the following command would create an app.js file.
    ```
    touch app.js
    ```
- Add the following starter code to the app.js file

  -

  ```
  	// Bring in Express code
  	const express = require('express')

  	const app = express()
  	const port = 3000

  	app.use(express.json()) // This line is necessary for Express to be able to parse JSON in request body's

  	app.get('/', (req, res) => {
  		res.send('Hello World!')
  	})

  	app.listen(port, () => {
  		console.log(`Example app listening on port ${port}`)
  	})
  ```

- ## Open your package.json file and find the object listed under "scripts", it should look like this:
  ```
  "scripts": {
  	"test": "echo \"Error: no test specified\" && exit 1"
  }
  ```
- ## Add a new script called "start" and set the value as "nodemon app.js"
  ```
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
  	"start": "nodemon app.js"
  }
  ```
  - _Commentary_: In a repository that has been initialized by npm, we can run predefined commands listed in the "scripts" of our package.json file by running the terminal command "npm {command-name}". Usually the command that is most often used is the "start" command which is used to start the project. In this case, we have defined the start command to run the terminal commands "nodemon app.js". Therefore, when we run the terminal command "npm start" it will run "nodemon app.js" and start our server.
- To test that all of this is working, run the "npm start" command in your terminal. You should see some nodemon output as well as the line "Example app listening on port 3000". This means your server is running and you can verify it by visiting localhost:3000 in your web browser. You should see the text "Hello World!" on it.
- Press control-c in the terminal to stop the server. Control-c can be used at any time in a terminal window to stop a process.
  - _Note_: Avoid exiting out of a terminal before a process has been stopped. Exiting out of the terminal closes the terminal window but does not necessarily stop the process itself. Use control-c to stop a process before exiting out of a terminal window.
- ## Commit your code and push your changes to github with the following commands
  ```
  	git add .
  	git commit -m "Initial Commit"
  	git push
  ```
  - _Commentary_:
    - The command "git add ." will stage all modified files in the current directory so that they can be committed to git. You can verify that the files had been added by running the "git status" command. Green files are the files that will be included in the commit, red files are files that will not be included in the commit.
    - The "git commit -m" command will create a new git commit. Git commits require a message be given to the commit. The -m flag allows you to add a message as a string to the commit.
    - Git push will push the commit from your local file system to your repository on github.
    - It is good practice to commit and push often, think of it as if you were saving a file except now your code is saved on github as well as your computer.
- Start your server again by running "npm start"
- Create a new postman collection called ExpressUserIntro
- Create a new request in the ExpressUserIntro collection that makes a request to "localhost:3000/", title this request "index route". Send the request and verify that "Hello World!" is recieved in the response.

- _Approach_: For all the following routes, we will using the following approach to develop them.
  1.  Create a Postman request that can send a HTTP request to the new route.
  2.  ## Create a new route in the app.js file. These new routes should go below the "/" route:
      ```
      app.get('/', (req, res) => {
      	res.send('Hello World!')
      })
      ```
      and above the app.listen() function:
  -
  ```
  app.listen(port, () => {
  	console.log(`Example app listening on port ${port}`)
  })
  ```
  - _Note_: When coding in a route, it is useful to test the variables and code you write with console.logs as you go.
    - To do this, make sure that at the end of the route you have either res.json({}) or res.send(''). This will ensure that you can make a request to the route without having the request hang (getting no response from the server).
    - Then send a request to the route with Postman. If you see a 404 Not Found error, that means your route was unable to be found. In that case, check that the route name in express and the route name in the url are both correct.
    - Once you have the above setup, you should be able to add console.logs in the route handler function, make a request to that particular route, and see the console.log output appear in the server terminal.

### 2) Read Routes

- Create a new Postman request in the ExpressUserIntro collection called "all-users". This request should make a GET request to localhost:3000/all-users.
- Create a new GET route that has the path "/all-users". Inside the route handler function, implement the following:
  - Respond to the request by sending the userList array.
- Test this route by sending the "all-users" postman request and verifying that the userList array is returned in the response.

- Create a new Postman request in the ExpressUserIntro collection called "single-user". This request should make a GET request to localhost:3000/single-user/(067) R85-9471.
- Create a new GET route that has the path "/single-user/:phoneNumber". Inside the route handler function, implement the following:

  - Get the phoneNumber property from the request route params.
  - Iterate through the userList array and find the user object that has the phone matching the phoneNumber from the route params.
    - _Hint_: There are many ways to accomplish this functionality. You can use a for loop to loop through userList and assign the matching user to a variable. You can also use an array method such as .findIndex() to find the index of the matching user and assign the user to a new variable with square bracket notation. Or even use the .find() method.
  - Respond to the request with the found user.

- Create a new Postman request in the ExpressUserIntro collection called "some-users". This request should make a GET request to localhost:3000/some-users/Ukraine.
- Create a new GET route that has the path "/some-users/:coutryName". Inside the route handler function, implement the following:
  - Get the phoneNumber property from the request route params.
  - Iterate through the userList array and find the user object that has the phone matching the phoneNumber from the route params.
    - _Hint_: There are many ways to accomplish this functionality. You can use a for loop to loop through userList and assign the matching user to a variable. You can also use an array method such as .filter()
  - Respond to the request with the found users.

### 3) Create Routes

- ## Create a new Postman request in the ExpressUserIntro collection called "new-user". This request should make a POST request to localhost:3000/new-user. In the Body section of the request set the input type dropdown to raw and then set the format type to JSON. Write a new JSON object in the body of one of your users with the following format:
  ```
  {
  	"gender": {String},
  	"name": {
  		title: {String},
  		first: {String},
  		last: {String},
  	},
  	"location": {
  		city: {String},
  		state: {String},
  		country: {String},
  		postcode: {Number},
  	},
  	"email": {String},
  	"phone": {Number},
  	"cell": {Number},
  	"nat": {String},
  }
  ```
  - _Commentary_: This POST request will send the JSON user object to the server inside the request body (req.body). When it comes to creating new data in the server, typically the data is sent in the body of a POST request. Once the data is received by the server, it is processed and then saved to a database.
- Create a new POST route that has the path "/new-user". Inside the route handler function, implement the following:

  - Create a new object that has the following properties representing a new user:
    ```
    const newUser = {
    	gender: {String},
    	name: {
    		title: {String},
    		first: {String},
    		last: {String},
    	},
    	location: {
    		city: {String},
    		state: {String},
    		country: {String},
    		postcode: {Number},
    	},
    	email: {String},
    	phone: {Number},
    	cell: {Number},
    	nat: {String},
    }
    ```
  - Push the new user object into the userList.
  - Respond to the request at the end of the route with an object that has the property "success" set to true
    - _Commentary_: When sending a response that performed some sort of operation that either created or updated data, we want to indicate whether or not the operation was a success. There are many reasons for why a data update operation was unsuccessful, maybe the data was invalid or maybe the database failed to properly update. By responding with success: true or success: false, we are letting the client that made the request know if their data was saved or not. Typically, after a client receives a successful or unsuccessful request, it will display a message to the user informing them of their request status.

  ```

  ```

- Test that this route is working properly by sending the "new-user" POST request with Postman with a new user in the request body. Then send a GET request to the "all-users" route to see if your new user made it into the userList array.

### 4) Update Routes

- ## Create a new Postman request in the ExpressUserIntro collection called "update-user". This request should make a PUT request to localhost:3000/update-user/{your-user-email} (replace {your-user-email} with the title of the user you created in the "new-user" request). In the Body section of the request set the input type dropdown to raw and then set the format type to JSON. Write a new JSON object in the body with the following format. The values should be different than the ones you had for "new-user".
  ```
  {
  	"gender": {String},
  	"name": {
  		title: {String},
  		first: {String},
  		last: {String},
  	},
  	"location": {
  		city: {String},
  		state: {String},
  		country: {String},
  		postcode: {Number},
  	},
  	"email": {String},
  	"phone": {Number},
  	"cell": {Number},
  	"nat": {String},
  }
  ```
- _Commentary_: You don't have to update every field, you just have to handle that in your server.
- Create a new PUT route that has the path "/update-user/:email". Inside the route handler function, implement the following:
  - Get the title of the user to update from the request route params.
  - Iterate through the userList array to find the object representing the original version of the user and assign it to a variable.
    - _Hint_: Use the .findIndex() method to find the index of the original user by looking for an object whose email matches the email coming from the route params. Then get the object by using square bracket notation.
  - Create a new object representing the updated version of the user.
  - For the fields, check to see if the value is defined on the request body. If it is, set that value on the updated user object. If it isn't, set the original value of the field on the updated user object.
    - _Commentary_: The idea here is to create an object that has either the original value for the user or the updated value. If the value has been provided in the request body, then we take that as the updated value. If the value has not been provided in the request body, then we want to keep the original value.
  - For the field createdAt, set this to the original value of createdAt in the updated user object.
  - Overwrite the original user object in the userList array with the updated user object.
  - Respond to the request at the end of the route with an object that has the property "success" set to true.
- Test that this route is working properly by sending the "update-user" PUT request with Postman with the updated user values in the request body. Then send a GET request to the "all-users" route to see if your user was updated in the userList array.

### 5) Delete Routes

- Create a new Postman request in the ExpressUserIntro collection called "delete-user". This request should make a DELETE request to localhost:3000/{your-user-cell} (replace {your-user-cell} with the cell of the user you created in the "new-user" request or the new title you gave that user in the "update-user" request).
- Create a new DELETE route that has the path "/delete-user/:cellNumber". Inside the route handler function, implement the following:
  - Get the cellNumber of the user to delete from the request route params.
  - Iterate through the userList array to find the index of the object whose cell matches the cellNumber to delete.
  - Remove the user at the found user index.
  - Respond to the request at the end of the route with an object that has the property "success" set to true.
- Test that this route is working properly by sending the "delete-user" DELETE request with Postman. Then send a GET request to the "all-users" route to see if your user was updated in the userList array.
