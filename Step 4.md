# MONGODB DATABASE
I will need a database where I will store our data. For this I will make use of mLab. mLab provides MongoDB database as a service solution [(DBaaS)]https://en.wikipedia.org/wiki/Cloud_database().

I will allow access to the MongoDB database from anywhere.
Create a MongoDB database and collection inside mLab
In the index.js file, I specified process.env to access environment variables, but I have not yet created this file. 

I will create a file in your Todo directory and name it .env.
```
touch .env
vi .env
```
Add the connection string to access the database in it, just as below:
```
DB = 'mongodb+srv://<username>:<password>@<network-address>/<dbname>?retryWrites=true&w=majority'
```
Ensure to update , 

Now I need to update the index.js to reflect the use of .env so that Node.js can connect to the database.

Simply delete existing content in the file, and update it with the entire code below.

To do that using vim, I'll:

Open the file with vim index.js
Press esc
Type :
Type %d
Hit ‘Enter’

The entire content will be deleted, then,

Now, I'll paste the entire code below in the file.
```
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

//connect to the database
mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
.then(() => console.log(`Database connected successfully`))
.catch(err => console.log(err));

//since mongoose promise is depreciated, we overide it with node's promise
mongoose.Promise = global.Promise;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use(bodyParser.json());

app.use('/api', routes);

app.use((err, req, res, next) => {
console.log(err);
next();
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
```
Using environment variables to store information is considered more secure and best practice to separate configuration and secret data from the application, instead of writing connection strings directly inside the index.js application file.
I'll Start your server using the command:
```
node index.js
```
I shall see a message ‘Database connected successfully’, if so – we have our backend configured. 

Testing Backend Code without Frontend using RESTful API So far I have written backend part of our To-Do application, and configured a database. I need ReactJS code to achieve that. But during development, I will need a way to test our code using RESTfulL API. Therefore, I will need to make use of some API development client to test our code.

In this project, I will use Postman to test our API. 


We should test all the API endpoints and make sure they are working. For the endpoints that require body, we should send JSON back with the necessary fields since it’s what we setup in our code.

Now I'll open your Postman, create a POST request to the API http://:5000/api/todos. This request sends a new task to our To-Do list so the application could store it in the database.


I'll Create a GET request to your API on http://:5000/api/todos. This request retrieves all existing records from out To-do application (backend requests these records from the database and sends it us back as a response to GET request).
We have successfully created our Backend, now let go create the Frontend.
