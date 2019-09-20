# Images, Fonts, and Files

Can just import a image and then the result will the final url after web pack

```js
import React from 'react';
import logo from './logo.png'; // Tell Webpack this JS file uses this image

console.log(logo); // /logo.84287d09.png

function Header() {
  // Import result is the URL of your image
  return <img src={logo} alt="Logo" />;
}

export default Header;
```

Or css

```css
.Logo {
  background-image: url(./logo.png);
}
```

### Can import SVG as component

All props are just dumped into the svg outer tag

```js
import { ReactComponent as Logo } from './logo.svg';
const App = () => (
  <div>
    {/* Logo is an actual React component */}
    <Logo width="40px" height="40px" className="checksvg" />
  </div>
);
```

*Included in create-react-app, but under the hood is [svgr](https://github.com/smooth-code/svgr)*

```scss
.checksvg {
  margin-right: $space-2s;

  path {
    stroke: $green;
    stroke-width: 2px;
  }
}
```

