# Gatsby

Check out the gatsby-**cli** for setup

Whats different about this then React?

- plugins simplify some things like configuration and shit
- Link
- Easy page/article adding(just add md, no routing needed)
- Data(anything outside code like Wordpress, css, markdown, apis, dbs) Integrations

## Basic Usage

#### Add new page

Just add a new file to `src/pages/name` and it will automatically be added to `localhost:8000/about`

#### Add a page layout

Just define a parent component and include it on every page using containment and `{{children}}`

#### Add new component

Make a `src/components`

Add and import files

## Special Gatsby Files

Must be found in root directory

Changes here require a rerun of `gatsby develop`

#### gatsby-broswer.js

```js
import "./src/styles/global.css"; //import global styles
```

#### gatsby-config.js

this is where you add plugins and other site configuration

```js
module.exports = {
  siteMetadata: {
    title: `Title from siteMetadata`,
  },
  plugins: [
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Options available to set within `gatsby-config.js` include:

1. [siteMetadata](https://www.gatsbyjs.org/docs/gatsby-config/#sitemetadata) (object)
2. [plugins](https://www.gatsbyjs.org/docs/gatsby-config/#plugins) (array)
3. [pathPrefix](https://www.gatsbyjs.org/docs/gatsby-config/#pathprefix) (string)
4. [polyfill](https://www.gatsbyjs.org/docs/gatsby-config/#polyfill) (boolean)
5. [mapping](https://www.gatsbyjs.org/docs/gatsby-config/#mapping-node-types) (object)
6. [proxy](https://www.gatsbyjs.org/docs/gatsby-config/#proxy) (object)
7. [developMiddleware](https://www.gatsbyjs.org/docs/gatsby-config/#advanced-proxying-with-developmiddleware) (function)

### Plugin Guide

Generally any npm package works

Plugins just offer easier integration 

Like  `Styled Components`, you could manually render the `Provider` component near the root of your application, or you could just use `gatsby-plugin-styled-components` which takes care of this step for you in addition to any other difficulties you may run into configuring Styled Components to work with server side rendering.