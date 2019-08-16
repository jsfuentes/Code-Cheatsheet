# Context

Share global data without passing through props, does make components less reusable

this.context will return the nearest ancestor's value of that context type, so can specialize further down tree

For multiple contexts, just add multiple providers and contexts if needed

## Usage

1) Create context(seperate file? theme-context.js)

2) Add Provider

3) Now any child component no matter how deep, can access by assigning a contextType

```js
const ThemeContext = React.createContext('light'); //default value

class App extends React.Component {
  render() {
    return (
      <ThemeContext.Provider value="dark"> //overrides default
        <Toolbar />
      </ThemeContext.Provider>
    );
  }
}

function Toolbar(props) {
  return <ThemedButton />;
}

class ThemedButton extends React.Component {
  static contextType = ThemeContext;

  render() {
    return <Button theme={this.context} />;
  }
}
```

Can also add Consumer to specific components that use the context

## Advanced

#### Updating Context and Consumers Example

Pass a ft with the context that lets you toggle it 

theme-context.js

```js
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

```js
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

```js
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