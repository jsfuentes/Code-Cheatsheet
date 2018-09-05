# Components

Try to get small, reusable components

function that takes Props and returns React component, a description of what to display that React then displays with `render`

**Cant change props**

```react
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

```react
const element = <Welcome name="Sara" />;
//OR
const x = "Sara";
const element = <Welcome name={x} />
//renders as: Hello, Sara
```

### Passing in props to children 

```react
<Component {...this.props} more="values" />
```



## Advanced

### Functional Components

Good style to just use a function when you don't need the state and other stuff

### Containment

Some components don't know who their children are like a border/sidebar

use special **children prop**, which pases anything inside the tags as props

```react
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}

function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
```

#### Need multiple Children?

Pass in as normal props then 

```react
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}
```

