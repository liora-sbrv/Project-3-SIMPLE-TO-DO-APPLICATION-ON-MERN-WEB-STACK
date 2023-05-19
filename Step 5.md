# FRONTEND CREATION
I want from our backend and API, it is time to create a user interface for a Web client (browser) to interact with the application via API. To start out with the frontend of the To-do app, I will use the create-react-app command to scaffold our app.

In the same root directory as my backend code, which is the Todo directory, I'll run:
```
npx create-react-app client
```
This will create a new folder in my Todo directory called client, where I will add all the react code.

Running a React App Before testing the react app, there are some dependencies that need to be installed.

I'll install concurrently. It is used to run more than one command simultaneously from the same terminal window.
```
npm install concurrently --save-dev
```
Install nodemon. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.
```
npm install nodemon --save-dev
```
In Todo folder open the package.json file. I'll change the highlighted part of the below screenshot and replace with the code below.
```
"scripts": {
"start": "node index.js",
"start-watch": "nodemon index.js",
"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
},
```
I'll configure Proxy in package.json

Then, change directory to ‘client’
```
cd client
```
Open the package.json file
```
vi package.json
```
Add the key value pair in the package.json file "proxy": "http://localhost:5000". The whole purpose of adding the proxy configuration in number 3 above is to make it possible to access the application directly from the browser by simply calling the server url like http://localhost:5000 rather than always including the entire path like http://localhost:5000/api/todos
```
npm run dev
```
Your app should open and start running on localhost:3000

Important note: In order to be able to access the application from the Internet you have to open TCP port 3000 on EC2 by adding a new Security Group rule. 

Creating our React Components One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. For our Todo app, there will be two stateful components and one stateless component. From Todo directory I run
```
cd client
```
I move to the src directory
```
cd src
```
Inside our src folder create another folder called components
```
mkdir components
```
I move into the components directory with
```
cd components
```
Inside ‘components’ directory I create three files Input.js, ListTodo.js and Todo.js.
```
touch Input.js ListTodo.js Todo.js
```
I'll open Input.js file
```
vi Input.js
```
And copy and paste the following
```
import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {

state = {
action: ""
}

addTodo = () => {
const task = {action: this.state.action}

    if(task.action && task.action.length > 0){
      axios.post('/api/todos', task)
        .then(res => {
          if(res.data){
            this.props.getTodos();
            this.setState({action: ""})
          }
        })
        .catch(err => console.log(err))
    }else {
      console.log('input field required')
    }

}

handleChange = (e) => {
this.setState({
action: e.target.value
})
}

render() {
let { action } = this.state;
return (
<div>
<input type="text" onChange={this.handleChange} value={action} />
<button onClick={this.addTodo}>add todo</button>
</div>
)
}
}

export default Input
```
To make use of Axios, which is a Promise based HTTP client for the browser and node.js, I will need to cd into my client from my terminal and run yarn add axios or npm install axios.

We will move to the src folder
```
cd ..
```
Then, move to clients folder
```
cd ..
```
Install Axios
```
npm install axios
```

