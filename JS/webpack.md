# Webpack

Compile javascript into bundles more efficiently managing dependencies(don't expect some library to already be included)

Out of the box handles js and json, use [loaders](https://webpack.js.org/concepts/#loaders) to add more file types(css, imgs)

*Use esbuild-loader for way faster building times*

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

A production web pack file

```js
const path = require("path");
const glob = require("glob");
const webpack = require("webpack");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
const CopyWebpackPlugin = require("copy-webpack-plugin");
const postcssNormalize = require("postcss-normalize");
const { ESBuildMinifyPlugin } = require("esbuild-loader");
const BundleAnalyzerPlugin =
  require("webpack-bundle-analyzer").BundleAnalyzerPlugin;
const conf = require("./conf");

const imageInlineSizeLimit = parseInt(
  process.env.IMAGE_INLINE_SIZE_LIMIT || "10000"
);

const paths = {
  appBuild: path.resolve(__dirname, "../priv/static"),
};

module.exports = (env, options) => ({
  optimization: {
    minimizer: [
      new ESBuildMinifyPlugin({
        target: "es2015",
        css: true, // Apply minification to CSS assets
      }),
    ],
  },
  entry: {
    "./src/app.js": glob.sync("./vendor/**/*.js").concat(["./src/app.tsx"]),
  },
  output: {
    filename: "[name]",
    chunkFilename: "src/[name][contenthash:8].chunk.js",
    path: paths.appBuild,
    // webpack uses `publicPath` to determine where the app is being served from.
    // It requires a trailing slash, or the file assets will get an incorrect path.
    // We inferred the "public path" (such as / or /my-project) from homepage.
    // ---------
    // webpack needs to know it to put the right <script> hrefs into HTML even in
    // single-page apps that may serve index.html for nested URLs like /todos/42.
    // We can't use a relative path in HTML because we don't want to load something
    // like /todos/42/static/js/bundle.7289d.js. We have to know the root.
    publicPath: conf.get("CLIENT_URL") + "/",
  },
  module: {
    rules: [
      {
        // "oneOf" will traverse all following loaders until one will
        // match the requirements. When no loader matches it will fall
        // back to the "file" loader at the end of the loader list.
        oneOf: [
          {
            test: /\.js$/,
            use: [
              {
                loader: "file-loader",
                options: {
                  name: "[name].[ext]",
                },
              },
            ],
            include: [
              path.resolve(
                __dirname,
                "node_modules/pdfjs-dist/legacy/build/pdf.worker.min.js"
              ),
            ],
          },
          // "url" loader works like "file" loader except that it embeds assets
          // smaller than specified limit in bytes as data URLs to avoid requests.
          // A missing `test` is equivalent to a match.
          {
            test: [/\.bmp$/, /\.gif$/, /\.jpe?g$/, /\.png$/],
            loader: require.resolve("url-loader"),
            options: {
              limit: imageInlineSizeLimit,
              name: "./media/[name].[hash:8].[ext]",
            },
          },
          {
            test: /\.(js|mjs|jsx)$/,
            exclude: /node_modules/,
            loader: "esbuild-loader",
            options: {
              loader: "jsx", // Remove this if you're not using JSX
              target: "es2015", // Syntax to compile to (see options below for possible values)
            },
          },
          {
            test: /\.tsx?$/,
            exclude: /node_modules/,

            loader: "esbuild-loader",
            options: {
              loader: "tsx", // Or 'ts' if you don't need tsx
              target: "es2015",
            },
          },
          {
            test: /\.css$/,
            use: [
              MiniCssExtractPlugin.loader,
              "css-loader",
              {
                loader: "postcss-loader",
                options: {
                  postcssOptions: {
                    ident: "postcss",
                    plugins: [
                      require("postcss-flexbugs-fixes"),
                      require("tailwindcss"),
                      require("postcss-preset-env")({
                        autoprefixer: {
                          flexbox: "no-2009",
                        },
                        stage: 3,
                      }),
                      // Adds PostCSS Normalize as the reset css with default options,
                      // so that it honors browserslist config in package.json
                      // which in turn let's users customize the target behavior as per their needs.
                      postcssNormalize(),
                    ],
                  },
                },
              },
            ],
          },
          {
            loader: require.resolve("file-loader"),
            // Exclude `js` files to keep "css" loader working as it injects
            // its runtime that would otherwise be processed through "file" loader.
            // Also exclude `html` and `json` extensions so they get processed
            // by webpacks internal loaders.
            exclude: [/\.(js|mjs|jsx|ts|tsx)$/, /\.html$/, /\.json$/],
            options: {
              name: "./media/[name].[hash:8].[ext]",
            },
          },
          // ** STOP ** Are you adding a new loader?
          // Make sure to add the new loader(s) before the "file" loader.
        ],
      },
    ],
  },
  plugins: [
    new webpack.EnvironmentPlugin(["NODE_ENV"]),
    new MiniCssExtractPlugin({ filename: "./src/app.css" }),
    new CopyWebpackPlugin({ patterns: [{ from: "public/", to: "./" }] }),
    new webpack.ProvidePlugin({
      process: "process/browser",
      React: "react",
    }), // https://stackoverflow.com/questions/41359504/webpack-bundle-js-uncaught-referenceerror-process-is-not-defined
    // Uncomment to fail webpack on typescript errors (and other errors)
    // function () {
    //   this.plugin("done", function (stats) {
    //     //Since webpack dependent Stats.js
    //     //Just see the API of Stats.js
    //     //You can do anything with the stats output
    //     if (stats && stats.hasErrors()) {
    //       stats.toJson().errors.forEach((err) => {
    //         console.error(err);
    //       });
    //       process.exit(1);
    //     }
    //   });
    // },
    //Uncomment to analyze your bundle
    // new BundleAnalyzerPlugin(),
  ],
  resolve: {
    modules: [path.resolve("./node_modules")],
    alias: {
      src: path.resolve("./src"),
      conf: path.resolve("./conf"),
    },
    extensions: [".tsx", ".ts", ".js"],
    fallback: {
      stream: require.resolve("stream-browserify"),
      crypto: require.resolve("crypto-browserify"),
      _stream_readable: require.resolve("readable-stream"),
    },
  },
});

```

### Visualizing

Create a viz of the libs increasing size of your bundle

```bash
yarn add -D webpack-bundle-analyzer
```

```js
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;
 
module.exports = {
  plugins: [
    new BundleAnalyzerPlugin()
  ]
}
```

