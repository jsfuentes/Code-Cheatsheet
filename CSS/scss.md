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
}
```

## Extra

To use variables in calc

```
body
    height: calc(100% - #{$body_padding})
```