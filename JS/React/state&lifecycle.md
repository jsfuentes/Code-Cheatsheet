# State and Lifecycle

Encapulsate changes in the compoonent

- Local **State** is dict like props, but **private** and fully controlled by component and not setup by React
- Can pass state down to child through props

## Lifecycle Hooks

- **Mounting** in React with `componentDidMount()`  runs when first rendering component to DOM
- **unmounting** with `componentWillUnmount()` runs before destroyed
- **update** with `componentDidUpdate(prevProps, prevState, snapshot)`
  - not initial render 

### Create a Ticking Clock

```react
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

#### Order of execution

1. `Constructor`
2. `Render` to DOM
3. `componentDidMount`
4. `Tick` called every second calling `setState()`
5. render() recalled b/c `setState()`
6. if compoonent removed, `componentWillUnmount`

## SetState()

Use setState() to set state, except in constructor

```react
// Wrong
this.state.comment = 'Hello';

// Correct, rerendering component
this.setState({comment: 'Hello'});
```

setState() is **async** and multiple calls could be buffer

Use overloaded setState() to rely on current state/props

```react
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});

// Correct
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
```

setState() merges given dict with current state overriding keys

```react
  constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }

  componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts //keeps comments intact
      });
    });
  }
```

### Usage

Data flows down, state can only affect components below

State vs stateless components are implementation detail and should be interchangeable

```react
<FormattedDate date={this.state.date} />
```

 