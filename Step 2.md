# STEP 2-INSTALL EXPRESSJS

To use express, I will install it using npm:
```
npm install express
```
Now I will create a file index.js with the command below
```
touch index.js
```
I will run ls to confirm that my index.js file is successfully created

I will install the dotenv module
```
npm install dotenv
```
I will open the index.js file with the command below
```
vim index.js
```
Will type the code below into it and save. 
```
const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
```
I have specified to use port 5000 in the code. This will be required later when we go on the browser.

Now it is time to start our server to see if it works. I will open my terminal in the same directory as my index.js file and type:
```
node index.js
```
If every thing goes well, we should see Server running on port 5000 in our terminal.
Now we need to open this port in EC2 Security Groups. 
We will open up our browser and try to access our server’s Public IP or Public DNS name followed by port 5000:
```
http://<PublicIP-or-PublicDNS>:5000
```
Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes
```
mkdir routes
```
I'll change directory to routes folder.
```
cd routes
```
Now,I will create a file api.js with the command below
```
touch api.js
```
I'll open the file with the command below
```
vim api.js
```
```
const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;
```
Moving forward we'll create Models directory.
