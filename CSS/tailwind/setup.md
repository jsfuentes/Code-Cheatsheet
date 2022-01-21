# Setup

Can use `npx tailwind build styles.css -o output.css`, but builtin cli doesn't include watch ability need postcss

### Setup

```bash
yarn add -D tailwindcss
npx tailwind init tailwind.config.js
yarn add -D postcss-cli autoprefixer
```

Add all the files names to content

```
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
  ],
```

postcss.config.js

```js
const tailwindcss = require("tailwindcss");

module.exports = {
  plugins: [tailwindcss("./tailwind.config.js"), require("autoprefixer")]
};
```

Autoprefixer is not required, but automatically tracks caniuse.com and properly prefixes(or unprefixes) css props

Tailwind replaces @tailwind directives with css

index.css

```css
@tailwind base;/* Preflight will be injected here */
/*Put all classes here*/
@tailwind components;
@tailwind utilities;
```

Preflight is opinionated and makes things like lists, h1, h2, etc unstyled by default

package.json

```json
"scripts": {
  "build:css": "postcss src/css/index.css -o src/index.css",
  "watch:css": "postcss src/css/index.css -o src/index.css -w",
  "start": "npm run watch:css & react-scripts start",
  "build": "npm run build:css && react-scripts build",
}
```

### Webpack

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

### Next

```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

