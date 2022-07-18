# Setting up React

## Installation

```bash
npm i react-dom
npm i react
```

Include html file with a root div

Add these script

```html
   <script src="https://unpkg.com/react@15/dist/react.min.js"></script>
   <script src="https://unpkg.com/react-dom@15/dist/react-dom.min.js"></script>
   <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/6.24.0/babel.js"></script>
   <script type="text/babel">
   ReactDOM.render(
       <div>Hello World</div>,
       document.getElementById("root")
   )
   </script>
```

react-scripts creates the root html page

## Create-react-app

```bash
npx create-react-app client
```

Check  `process.env.NODE_ENV`  for the current environment either "production" when built or "development"

To set all imports to be absolute "components/CTA.js" instead of "../components/CTA.js", add the following file to the root(package.json level) dir

jsconfig.json

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "ES6",
    "jsx": "preserve",
    "checkJs": true,
    "baseUrl": "./src"
  },
  "exclude": ["node_modules", "**/node_modules/*"]
}
```

## Setup With Node

```bash
mkdir node-react-app && cd node-react-app
npx create-react-app client
npx express-generator backend --no-view
cd backend && npm install
```

In `backend/bin/www`,  change the default port number to 3001

In `client/package.json` add `  "proxy": "http://localhost:3001"` to the json

Now in the main folder fullstack_app:

```bash
npm init -y 
npm i concurrently
```

In `package.json`, add `"start": "concurrently \"cd backend && npm run start\" \"cd client && yarn start\""`  under scripts

Now just `npm run start` in the main folder

#### Docker

Use docker-compose to get two containers up, use `"proxy": "http://[service-name]:[port-number]"` instead

### Gotchas

Express generator comes with express.json bodyparsering which is a much less lenient form of post request processing then the bodyparser package(must specify application/json header)

Nodemon needs to be added

React-generator uses yarn and has a yarn.lock, it became a problem

