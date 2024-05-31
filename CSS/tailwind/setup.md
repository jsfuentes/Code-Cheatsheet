# Setup

Can use `npx tailwind build styles.css -o output.css`, but builtin cli doesn't include watch ability need postcss

### Setup

```bash
yarn add -D tailwindcss postcss-cli autoprefixer
npx tailwind init tailwind.config.js
```

Add all the files names to content

```
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
  ],
```

Tailwind replaces @tailwind directives with css

index.css

```css
@tailwind base;/* Preflight will be injected here */
/*Put all classes here*/
@tailwind components;
@tailwind utilities;
```

Preflight is opinionated and makes things like lists, h1, h2, etc unstyled by default

If you're using Next.js you're done, if you using webpack or react-scripts see below

#### More For React-Scripts

postcss.config.js

```js
const tailwindcss = require("tailwindcss");

module.exports = {
  plugins: [tailwindcss("./tailwind.config.js"), require("autoprefixer")]
};
```

Autoprefixer is not required, but automatically tracks caniuse.com and properly prefixes(or unprefixes) css props

package.json

```json
"scripts": {
  "build:css": "postcss src/css/index.css -o src/index.css",
  "watch:css": "postcss src/css/index.css -o src/index.css -w",
  "start": "npm run watch:css & react-scripts start",
  "build": "npm run build:css && react-scripts build",
}
```

#### More for Webpack

Tailwind >1.4 does purging if NODE_ENV=production

```js
          {
            test: /\.css$/,
            use: [
              MiniCssExtractPlugin.loader,
              "css-loader",
              {
                loader: "postcss-loader",
                options: {
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
            ],
          },
```

### React Native

Need to use [nativewind](https://www.nativewind.dev/quick-starts/expo)

```bash
npm i nativewind
npm i -D tailwindcss
npx tailwindcss init
```

tailwind.config.js

```ts
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ['./App.{js,jsx,ts,tsx}', './src/**/*.{js,jsx,ts,tsx}'],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

babel.config.js

```ts
+   plugins: ["nativewind/babel"]
```

Now adding className to something will transform it into a styled tailwindcss component

Add the below to an app.d.ts to avoid type errors

```ts
/// <reference types="nativewind/types" />
```

