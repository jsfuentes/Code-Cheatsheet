# TailwindCss

#### Copied from CSS/tailwindcss

```bash
yarn add -D tailwindcss autoprefixer cssnano
npx tailwind init tailwind.config.js --full
```

Create the css file somewhere

```css
@tailwind base;/* Preflight will be injected here */
/*Put all classes here*/
@tailwind components;
@tailwind utilities;
```

#### Gatsby Specific

```bash
yarn add gatsby-plugin-postcss
```

gatsby-browser.js

```js
require("./static/css/index.css");
```

Gatsby-config.js

```js
const tailwindConfig = require("./tailwind.config.js");

    {
      resolve: `gatsby-plugin-postcss`,
      options: {
        postCssPlugins: [
          require(`tailwindcss`)(tailwindConfig),
          require(`autoprefixer`),
         ...(process.env.NODE_ENV === `production`
            ? [require(`cssnano`)]
            : []),
        ],
      },
    },
```

