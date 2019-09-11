# Scss

A superset of css that compiles to css

- importing
- Variables with $ 
- Groups/modularity

Can use node-sass to compile withs css

```scss
@import url('https://fonts.googleapis.com/css?family=Poppins:300,400,600&display=swap');
$black: #2E2E2E;
$primary: #E95D5D;

$body-font: calc(2.1vh);
$input-font: calc(2.1vh);

.button-container{
	margin-top: 2em;
	text-align: center;
	
  //I think equivalent to 
  //.button-container input[type="submit"] {....}
	input[type="submit"]{
		text-align: center;
		background-color: $primary;
		font-size: $input-font;
  }
  
  //equivalent to button-container:hover
  &:hover { 
        transform: scale(1.01, 1.01);
  }
}
```

#### Importing

Partials have leading underscore and can be used with 

```scss
@import 'spacing.scss'
```

_spacing.scss

```
#stuff
```

## Extra

To use variables in calc

```
body
    height: calc(100% - #{$body_padding})
```

#### Math

```scss
article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}
```

## Installation

```bash
yarn add node-sass	
```

In create react app, just install and it will start working on import 

Can also just use node-sass

```json
{
	"build:css": "node-sass --omit-source-map-url src/css/style.scss src/css/style.css",
	"watch:css": "npm run build:css -- --watch",
}
```



