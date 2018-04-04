# Setup for Nodejs/Express

`node` will work if you have node

## Using Generator
```bash
npm install express-generator -g
express [project name] --ejs
```
- --view=ejs adds ejs engine support
- --git adds a gitignore  



## Running
with nodemon
`npm install -g nodemon`
`nodemon ./server.js localhost 8080`

## Morgan
it is for automated logging of requests, responses and related data


#### Running Other Commands
Other command add the following script block to our package.json file (assuming that our application source is in a folder /src/js):

"scripts": {
  ...
  "lint": "eslint src/js"
  ...
}
