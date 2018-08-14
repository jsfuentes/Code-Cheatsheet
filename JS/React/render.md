# rendering

```react
import React from 'react';
import ReactDOM from 'react-dom';

const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

## Update Rendering

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

## Conditional Rendering

Simple

```react
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);
```

Can also use inline logic see jsx

