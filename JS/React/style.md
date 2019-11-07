# Style

## Inline

```js
<p style={{transform: 'scale(0.5, 0.5)'}}> ... </p>
```

## CSS Modules

Keep all styles scoped to that component

```js
import React from 'react';
import styles from './DashedBox.css';

const DashedBox = () => (
  <div className={styles.container}>
    <p className={styles.content}>Get started with CSS Modules style</p>
  </div>
);

export default DashedBox;
```

#### DashedBox

```css
 :local(.container) {
   margin: 40px;
   border: 5px dashed pink;
 }
 :local(.content) {
   font-size: 15px;
   text-align: center;
 }
```

`:local(.className)`-this when you use create-react-app because of webpack configurations

`.className`-this if you use your own react boilerplate and you need to add some webpack configuration idk

Learn about it [here](https://medium.com/@pioul/modular-css-with-react-61638ae9ea3e#.re1pdcz87)

## Import

```bash
import './DottedBox.css';
```

#### SCSS

```bash
npm install node-sass -S
```

```js
import './DottedBox.scss';
```

## CSS-in-JS(inline)

No dash allowed so border-left becomes borderLeft

```jsx
import React from 'react';

const divStyle = {
  margin: '40px',
  border: '5px solid pink'
};
const pStyle = {
  fontSize: '15px',
  textAlign: 'center'
};

const Box = () => (
  <div style={divStyle}>
    <p style={pStyle}>Get started with inline style</p>
  </div>
);

export default Box;
```

### Libraries

Emotion

