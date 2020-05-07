# Webpack

Compile javascript into bundles more efficiently managing dependencies(don't expect some library to already be included)

Out of the box handles js and json, use [loaders](https://webpack.js.org/concepts/#loaders) to add more file types(css, imgs)

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

### Add Images

```
npm install file-loader url-loader
```

```js
	module: {
	  rules: [
	  //....
      {
        test: [/\.bmp$/, /\.gif$/, /\.jpe?g$/, /\.png$/],
        loader: require.resolve("url-loader"),
        options: {
          limit: imageInlineSizeLimit,
          name: "../priv/static/media/[name].[hash:8].[ext]",
        },
      },
    ],
  },
```

### Examples

Simple example from elixir 

```js
const path = require("path");
const glob = require("glob");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
const TerserPlugin = require("terser-webpack-plugin");
const OptimizeCSSAssetsPlugin = require("optimize-css-assets-webpack-plugin");
const CopyWebpackPlugin = require("copy-webpack-plugin");

module.exports = (env, options) => ({
  optimization: {
    minimizer: [
      new TerserPlugin({ cache: true, parallel: true, sourceMap: false }),
      new OptimizeCSSAssetsPlugin({}),
    ],
  },
  entry: {
    "./js/app.js": glob.sync("./vendor/**/*.js").concat(["./js/app.js"]),
  },
  output: {
    filename: "app.js",
    path: path.resolve(__dirname, "../priv/static/js"),
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
        },
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader"],
      },
    ],
  },
  plugins: [
    new MiniCssExtractPlugin({ filename: "../css/app.css" }),
    new CopyWebpackPlugin([{ from: "public/", to: "../" }]),
  ],
  //added resolve allowing absolute path imports from 'js/...' 
  resolve: {
    modules: [path.resolve("./node_modules")],
    alias: {
      js: path.resolve("./js"), 
    },
  },
});
```

