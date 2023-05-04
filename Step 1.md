# STEP 1 – BACKEND CONFIGURATION
Update ubuntu
```
sudo apt update
```
Lets get the location of Node.js software from Ubuntu repositories.
```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
I will install Node.js on the server Install Node.js with the command below
```
sudo apt-get install -y nodejs
```
The command above installs both nodejs and npm. NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.

I will verify the node installation with the command below

```
node -v 
```
I will verify the node installation with the command below
```
npm -v
```
Application Code Setup Create a new directory for your To-Do project:
```
mkdir Todo
```
I will run the command below to verify that the Todo directory is created with ls command
```
ls
```
In order to see some more useful information about files and directories, we can use following combination of keys ls -lih – it will show us different properties and size in human readable format. 

Now I change my current directory to the newly created one:
```
cd Todo
```
Next, I will use the command npm init to initialise my project, so that a new file named package.json will be created. This file will normally contain information about my application and the dependencies that it needs to run.
```
npm init
```
I will run the command ls to confirm that I have package.json file created.

Next, we will Install ExpressJs and create the Routes directory.
