# Deployment

## Simplest

Assuming create-react-app, you need to build with `yarn build` then you can just statically serve the build folder's index.html

```js
const express = require('express');
const path = require('path');
const app = express();

app.use(express.static(path.join(__dirname, 'build')));

app.get('/', function(req, res) {
  res.sendFile(path.join(__dirname, 'build', 'index.html'));
});

app.listen(9000);
```

## Express Server

```js
app.get('/*', function (req, res) {
   res.sendFile(path.join(__dirname, 'build', 'index.html'));
 });
```

When developing, inside client/package.json for the create-react-app web pack

```
"proxy": "http://localhost:3001/",
```

Then you can simply

```js
fetch(`/api/food`....
```

Then although the react app is running on 3000, api request like above will be sent to 3001. And in production, this will appriorately just hit the main domain :)