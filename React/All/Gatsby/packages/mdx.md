# MDX

```bash
yarn add gatsby-plugin-mdx @mdx-js/mdx @mdx-js/react
yarn add gatsby-source-filesystem # frontmatter, generate Gatsby nodes from local files, and use import/export functionality in our MDX files
```

gatsby-config.js

```js
module.exports = {
  //...siteMetadata, etc
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `pages`,
        path: `${__dirname}/src/pages/`,
      },
    },
    {
      resolve: `gatsby-plugin-mdx`,
      options: {
        defaultLayouts: {
          default: require.resolve(`./src/components/Layout`),
        },
      },
    },
    // ... other plugins
  ],
}
```

