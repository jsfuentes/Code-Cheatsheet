# React

Given design:

1) Break UI into component hierarchy

2) Build Static version in react(no state, state for interactivity)

3) Identify The Minimal (but complete) Representation Of UI State(calculate computed terms on render and remember if its passed in as props then its the parent's job to change it)

4) Identify where state should live

5) Add Inverse Data Flow, pass update fts to lower components

### Data Flow

Data flows down from parent to child, so if multiple components have a shared state put it in the closest common ancestor

Notice if we rerender a parent component with setState() all the children get rerendered (if needed?)

If something can be derived from either props or state, it probably shouldn’t be in the state.

### Thinking about React

- Data flows down from parent to child
- Try to get small, reusable components
- Components take props and return react component

- Passing props for specialization is equivalent of composition/inheritance (i.e create WelcomeDialog by passing in specific props to Dialog)
- can even pass other components in props and choose what to do with it

```jsx
function FancyBorder(props) {
  return (
    <div className={'FancyBorder'}>
      {props.children}
    </div>
  );
}

function WelcomeDialog() {
  return (
    <FancyBorder>Welcome</FancyBorder>
  );
}
```

Need multiple children??

```jsx
function SplitPane(props) {
  return (
    <div className="w-full h-full flex">
      <div className="h-1/2">{props.left}</div>
      <div className="h-1/2">{props.right}</div>
    </div>
  );
}

function App() {
  return (
    <SplitPane 
      left={<Contacts />} 
      right={<Chat />  } 
    />
  );
}
```

# Components

**Cant change props**

```jsx
import React from "react"; //jsx support
//Functional component - Good style when no need for advanced stuff
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

//has constructor, state&lifecycle stuff
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

## Using Components

If you have user defined component(capitalized) in JSX, passes in props

```jsx
const element = <Welcome name="Sara" />;
//OR
const x = "Sara";
const element = <Welcome name={x} />
//renders as: Hello, Sara
```

### Passing in props to children 

```jsx
<Component {...this.props} more="values" />
```

## Example

Lets say we are trying to make a F & C temp indicator

##### Temperature Input for F or C

```jsx
class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(e) {
    this.props.onTemperatureChange(e.target.value);
  } //notice call ft from props

  render() {
    const temperature = this.props.temperature;
    const scale = this.props.scale; //notice dynamic based on props
    return (
      <fieldset>
        <legend>Enter temperature in {scaleNames[scale]}:</legend>
        <input value={temperature}
               onChange={this.handleChange} />
      </fieldset>
    );
  }
}
```

##### Temp Calculator

```jsx
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleCelsiusChange = this.handleCelsiusChange.bind(this);
    this.handleFahrenheitChange = this.handleFahrenheitChange.bind(this);
    this.state = {temperature: '', scale: 'c'};
  }

  handleCelsiusChange(temperature) {
    this.setState({scale: 'c', temperature});
  }

  handleFahrenheitChange(temperature) {
    this.setState({scale: 'f', temperature});
  }

  render() {
    const scale = this.state.scale;
    const temperature = this.state.temperature;
    const celsius = scale === 'f' ? tryConvert(temperature, toCelsius) : temperature;
    const fahrenheit = scale === 'c' ? tryConvert(temperature, toFahrenheit) : temperature;

    return (
      <div>
        <TemperatureInput
          scale="c"
          temperature={celsius}
          onTemperatureChange={this.handleCelsiusChange} />
        <TemperatureInput
          scale="f"
          temperature={fahrenheit}
          onTemperatureChange={this.handleFahrenheitChange} />
        <BoilingVerdict
          celsius={parseFloat(celsius)} />
      </div>
    );
  }//notice the props passed in including a ft
}
```

