# Boxicons

```
$ npm install boxicons --save
```

Import the npm module in your javascript

```js
import 'boxicons'
```

And link css

```html
    <link href='https://unpkg.com/boxicons@2.0.8/css/boxicons.min.css' rel='stylesheet'>

```

## Usage

```jsx
<div className="bx bx-loader-alt animate-spin mr-2" />
```

[LIST](https://boxicons.com/)

```jsx
<box-icon type="solid" name="rocket"></box-icon>
<box-icon type="logo" name="facebook-square"></box-icon>
```

The `box-icon` custom element supports the following attributes:

```jsx
<box-icon
type = "regular|solid|logo"
name="adjust|alarms|etc...."
color="blue|red|etc..."
size="xs|sm|md|lg|cssSize"
rotate="90|180|270"
flip="horizontal|vertical"
border="square|circle"
animation="spin|tada|etc..."
animation="spin|tada|etc..."
pull = "left|right"
></box-icon>
```

