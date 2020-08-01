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

## 