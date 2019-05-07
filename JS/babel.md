#  Babel

Babel complies the new js depencies down to basic js allowing it to be used across browsers 

No real competition, this is it baby

Usually uses a plugin system where you need to install individual plugins to use a specific new feature

Webpack or browserify will do this auto

### Babel Standalone 

A nice collection of babel and plugins

```html
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
<!-- Your custom script here -->
<script type="text/babel">
const getMessage = () => "Hello World";
document.getElementById('output').innerHTML = getMessage();
</script>
```

#### Load External Scripts

```html
<script type="text/babel" src="foo.js"></script>
```

#### Command LIne

You can install a babel cli and run the command to compile it and see it yourself