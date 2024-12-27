# Context

Share global data without passing through props, does make components less reusable

this.context will return the nearest ancestor's value of that context type, so can specialize further down tree

For multiple contexts, just add multiple providers and contexts if needed

## Usage

1) Create context(seperate file? theme-context.js)

PizzaContext.js

```jsx
import React from "react";

const ThemeContext = React.createContext('light'); //default value

export default ThemeContext;
```

2) Add Provider

```jsx
function App(){
  return (
    <ThemeContext.Provider value="dark"> //overrides default
    <Toolbar />
    </ThemeContext.Provider>
  );
}
```

3) Now anything in subtree of Provider can access data

- useContext hook can access data

```jsx
import ThemeContext from "./ThemeContext";

export default function Pizza(props) {
	const theme = useContext( ThemeContext );
  
  return <div>{theme}</div>;
}
```

- Contexttypes can access data in classes

```jsx
import ThemeContext from "./ThemeContext";

class ThemedButton extends React.Component {
  static contextType = ThemeContext;

  render() {
    return <Button theme={this.context} />;
  }
}
```

## Advanced

#### Updating Context and Consumers Example

Pass a ft with the context that lets you toggle it 

theme-context.js

```jsx
export const themes = {
  light: { foreground: '#000000 },
  dark: {foreground: '#ffffff' },
};

//default should match type of expected
export const ThemeContext = React.createContext({
  theme: themes.dark,
  toggleTheme: () => {},
});
```

**theme-toggler-button.js**

```jsx
import {ThemeContext} from './theme-context';

function ThemeTogglerButton() {
  return (
    <ThemeContext.Consumer>
      {({theme, toggleTheme}) => (
        <button
          onClick={toggleTheme}
          style={{backgroundColor: theme.background}}>
          Toggle Theme
        </button>
      )}
    </ThemeContext.Consumer>
  );
}

export default ThemeTogglerButton;
```

**app.js**

```jsx
import {ThemeContext, themes} from './theme-context';
import ThemeTogglerButton from './theme-toggler-button';

class App extends React.Component {
  constructor(props) {
    super(props);

    this.toggleTheme = () => {
      this.setState(state => ({
        theme:
          state.theme === themes.dark
            ? themes.light
            : themes.dark,
      }));
    };
    
    this.state = {
      theme: themes.light,
      toggleTheme: this.toggleTheme,
    };
  }

  render() {
    return (
      <ThemeContext.Provider value={this.state}>
        <Content />
      </ThemeContext.Provider>
    );
  }
}

//some intermidate components
function Content() {
  return (
    <div>
      <ThemeTogglerButton />
    </div>
  );
}

ReactDOM.render(<App />, document.root);
```



### 