# Basics

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

## Setup With Node

```bash
mkdir fullstack_app && cd fullstack_app
npm i -g create-react-app
create-react-app client && cd client
cd ..
express backend --no-view
cd backend && npm install
```

Change port of express server in /bin to 3001

Add `  "proxy": "http://localhost:3001",` to npm start in the client 

Now in the main folder fullstack_app:

```bash
npm init -y 
npm i concurrently
concurrently \"cd backend && npm start\" \"cd client && npm start\"
```

#### Docker

Use docker-compose to get two containers up, use `"proxy": "http://[service-name]:[port-number]"` instead