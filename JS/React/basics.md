# Basics

`npm install -g create-react-app`

`create-react-app my-app`

### Simplest Example

```js
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

react-scripts creates the root html page

## JSX

- Combines logic with display
- Can put any js expression within braces in JSX
- React elements are immutable js objects
- Camel case: 
  - class => className 
  - tabindex => tabIndex

```react
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

const element = <img src={user.avatarUrl} />;
//either use quote or js expression
```

*auto esapes values in JSX to prevent XSS*

#### JSX transform

```react
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
//jsx becomes
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
//which essentially becomes
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

## rendering

```react
import React from 'react';
import ReactDOM from 'react-dom';

const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

### Update Rendering

- Need to create new element to change
- Virtual DOM changes only whats needed

```react
function tick() {
  const element = (
    <div>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);
```

## Components

Try to get small, reusable components

function that takes Props and returns React component

**Cant change props**

```react
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### Using Components

If you have user defined component(capitalized) in JSX, passes in props

```react
const element = <Welcome name="Sara" />;
//renders as: Hello, Sara
```











```react
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// Example usage: <ShoppingList name="Mark" />
```

A component takes in parameters, called `props` , and returns a hierarchy of views to display via the `render` method.

`render` method returns a *description* of what you want to see on the screen. React takes the description and displays the result.