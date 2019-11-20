# Events

## Differences from HTML

- camelCase events, rather than lowercase 
- pass a function as the event handler, rather than a string 

```html
<!-- HTML -->
<button onclick="activateLasers()">
  Activate Lasers
</button>
```

becomes

```react
//React
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

#### PreventDefault

call `preventDefault` rather then return false

 ```HTML
<!-- HTML -->
<a href="#" onclick="console.log('The link was clicked.'); return false">
  Click me
</a>
 ```

becomes

```react
//React
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```

e is a synthetic event handling cross-browser compat

## Usage

Pass functions into event handlers

- use `event.persist();` if you access async because react event objects are recycled so could be different

```react
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

### Bind()

`[method].bind(this)`  is a vanilla JS function that sets the `this` ptr of the function to the arg passed needed when passing ft like in callbacks rather than calling it

Generally, if you refer to a method without `()` after it, such as `onClick={this.handleClick}`, you should bind that method.

##### Not using bind()?

```react
class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.
  // Warning: this is *experimental* syntax.
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

### Passing arg to Event Handler

```react
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

Equivalent using arrow fts and bind respectively, e will be 2nd arg in both