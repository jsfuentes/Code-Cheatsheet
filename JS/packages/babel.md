#  Babel

Babel complies the new js depencies down to basic js allowing it to be used across browsers 

No real competition, this is it baby

you install individual plugins to get any features and set `.babelrc` or `babel.config.js` or something

Webpack or browserify will do this auto

**Watch out, all the babel 6 guides have all the plugins/extensions use something like `babel-preset-env` while babel 7 changed everything to `@babel/preset-env`**

## Super Basic

### Babel Standalone 

A nice collection of babel and plugins

```html
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
<!-- Your custom script here -->
<script type="text/babel">
const getMessage = () => "Hello World";
document.getElementById('output').innerHTML = getMessage();
</script>
```

#### Load External Scripts

```html
<script type="text/babel" src="foo.js"></script>
```

#### Command LIne

You can install a babel cli and run the command to compile it and see it yourself

## Basic Configuration

- You want to programmatically create the configuration?
- You want to compile `node_modules`?

> [`babel.config.js`](https://babeljs.io/docs/en/configuration#babelconfigjs) is for you!

- You have a static configuration that only applies to your simple single package?

> [`.babelrc`](https://babeljs.io/docs/en/configuration#babelrc) is for you!

```json
{
  plugins: ["@babel/plugin-transform-runtime"]
}
```

You just add npm install the plugin and add it to this list

##### Async/Await Runtime

```bash
npm install --save @babel/runtime
```

```sh
npm install --save-dev @babel/plugin-transform-runtime
```

Add this as a plugin as above

### Presets

Groups of plugins

#### babel-preset-env

`npm install --save-dev @babel/preset-env`

.babelrc

```json
{
  "presets": [
    ["env", {
      "targets": {
        "browsers": ["last 5 Chrome versions"]
      }
    }]
}
```

Allows you to specify the specific browsers to support which can greatly simplify file size

*source maps are to allow debugging in the console to the correct lines*

### Good default

 `@babel/core @babel/cli` do nothing alone

`babel-loader` is for web pack usage and configuration

`babel-preset-react` is for react stuff

```bash
npm install --save-dev babel-loader babel-core babel-preset-react babel-preset-env babel-plugin-transform-runtime

npm install --save babel-runtime
```

.babelrc

```json
{
  "presets": [
    ["env", "targets": {
        "browsers": ["defaults"]
      }],
    "react"
  ],
  "plugins": [
    "transform-runtime"
  ]
}
```

