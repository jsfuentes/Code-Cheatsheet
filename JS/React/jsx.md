## JSX

- Combines logic with display

- Can put **any** js expression within braces in JSX

- React elements are immutable js objects

- ```react
  const name = 'Josh Perez';
  const element = <h1>Hello, {name}</h1>;
  
  const element = <img src={user.avatarUrl} />;
  //either use quote string or js expression
  ```

  *auto esapes values in JSX to prevent XSS*

  

## Syntax

- Can close empty tags with /> i.e `<img src=... />`
- Camel case: 
  - class => className 
  - tabindex => tabIndex
- Can have nested divs, but must have a single outermost div
- Can be multiple lines

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

### Rendering with Variable

```react
let button = <LogoutButton onClick={this.handleLogoutClick} />;
return (  <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
```

### Inline Logic 

```react
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}
```

```react
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
    </div>
  );
}
```

### Prevent Component from Rendering

just return null

```react
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Warning!
    </div>
  );
}
```

