# Webpack

Compile javascript into bundles more efficiently managing dependencies(don't expect some library to already be included)

```bash
npm install webpack --save-dev
npm install webpack-cli --save-dev
```

**webpack.config.js**

```js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

