# README

Gatsby is a static site generator with plugins and makes adding pages easy

- Gatsby dictates how you should handle data in your app.

[Next](https://nextjs.org/) seems even better allowing easy page adding, mainly server side rendered pages, also supports static site generation

- Managing data up to you 

## Basics

`npx create-react-app my-app`

## Thinking about React

- Data flows down from parent to child

- Passing props for specialization is equivalent of composition/inheritance, 

- can even pass other components in props and choose what to do with it

Given design:

1) Break UI into component hierarchy

2) Build Static version in react(no state, state for interactivity)

3) Identify The Minimal (but complete) Representation Of UI State(calculate computed terms on render and remember if its passed in as props then its the parent's job to change it)

4) Identify where state should live

5) Add Inverse Data Flow, pass update fts to lower components

## Installation

`npm i react-dom`

`npm i react`

Include html file with a root.js

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