# Forms

## Controlled Components

Normally form elements such as `<input> `maintain their own state and update based on input. To combine with React state, let React state be the “single source of truth” by updating it on change

- React makes different tags like select, textarea, and text all have value attribute with similar code for a controlled component
- specify `value` to prevent user from changing input, set to null/undefined to make re editable

```react
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) { 
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value //es6 computed property syntax
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```

## Custom Hooks

```js
const useSearch = (callback) => {
    const [inputs, setInputs] = useState({});

    const handleSubmit = (event) => {
        if (event) {
        event.preventDefault();
        }
        callback(event);
    }

    const handleInputChange = (event) => {
        event.persist();
        setInputs(inputs => ({...inputs, [event.target.name]: event.target.value}));
    }

    return {
        handleSubmit,
        handleInputChange,
        inputs
    };
}
```

Then



## Specific Tags

#### Select

```html
<!--HTML-->
<select>
  <option selected value="coconut">Coconut</option>
  <option value="mango">Mango</option>
</select>
```

becomes

```react
<select value={this.state.value} onChange={this.handleChange}>
    <option value="coconut">Coconut</option>
    <option value="mango">Mango</option>
</select>
```

Recall selected attribute in HTML choose what is initallly selected, value on main select tag does that in React

*select multiple with <select multiple={true} value={['B', 'C']}>*

### Un Controlled

`<input type="file" />` 

look above tedious b/c integrating with nonReact or converting codebase