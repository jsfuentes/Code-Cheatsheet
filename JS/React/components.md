# Components

Try to get small, reusable components

In: Props 

Out: React component displayed by running render

**Cant change props**

```react
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

## Class Components

```js
export default class Chat extends Component {
  constructor(props) {
    super(props); //needed
    //only place you can just use this.state to set
    this.state = { 
      messageHistory: [],
      nextMessage: null
    };

    //binding this ptr
    this.submitOption= this.submitOption.bind(this);
    this.getChromeStorage = this.getChromeStorage.bind(this);
  }

  componentDidMount() {
    this.getChromeStorage();
  }

  componentDidUpdate() {
    this.msgAnchor.scrollIntoView({ behavior: 'smooth' });
  }

  render() {
    //....
  }
}
```

## Advanced

#### Specialization

Specialized component like welcome dialog render a more general dialog component using props heavily and holding state, maybe general is just functional and reusable

#### Containment

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

