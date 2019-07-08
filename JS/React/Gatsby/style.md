# Style

Can add /style folder, css files, then import globally in `gatsby-browser.js`

 [Check out the docs](https://www.gatsbyjs.org/docs/creating-global-styles/#how-to-add-global-styles-in-gatsby-with-standard-css-files)

## CSS Modules

This seems different than pure React CSS modules

If you console.log the imported style, you see it just maps to globally unique name generated 

```json
{
	container: "about-css-modules-module—container—bPeug"
}
```

src/components/container.js

```javascript
import React from "react"
import containerStyles from "./container.module.css"

export default ({ children }) => (
  <div className={containerStyles.container}>{children}</div>
)
```

src/components/container.module.css

```css
.container {
  margin: 3rem auto;
  max-width: 600px;
}

.container:hover {
  background-color: rebeccapurple;
}
```

pages/test.js

```js
import React from "react"
import styles from "./about-css-modules.module.css" //add custom css here too
import Container from "../components/container"

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
  </Container>
)
```

Need `.module.css` suffix to tell Gatsby its a module

### CSS-in-JS

https://speakerdeck.com/vjeux/react-css-in-js

Its a thing

