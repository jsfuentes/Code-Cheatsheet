# Plugins

[Library](https://www.gatsbyjs.org/plugins/)

## List of Plugins for React Packages

These usually just allow easier integration

- Emotion: Adds `/** @jsx jsx */` to files
- Typography: style component of typography is automatically inserted into the head by the plugin

```js
module.exports = {
  plugins: [
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

## Example Typography

The style component of typography is automatically inserted into the head by the plugin

```bash
npm install --save gatsby-plugin-typography react-typography typography typography-theme-fairy-gates
```

gatsby-config.js

```javascript
module.exports = {
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

src/utils/typography.js

```javascript
import Typography from "typography"
import fairyGateTheme from "typography-theme-fairy-gates"

const typography = new Typography(fairyGateTheme)

export const { scale, rhythm, options } = typography
export default typography
```