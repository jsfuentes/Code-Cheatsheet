# Sass

A superset of css that compiles to css

Adds variables and groups

```scss
@import url('https://fonts.googleapis.com/css?family=Poppins:300,400,600&display=swap');
$black: #2E2E2E;
$primary: #E95D5D;

$body-font: calc(2.1vh);
$input-font: calc(2.1vh);

.button-container{
	margin-top: 2em;
	text-align: center;

	input[type="submit"]{
		text-align: center;
		background-color: $primary;
		font-size: $input-font;
  }
}
```

