## Simplest Example

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
