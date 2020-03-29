# Forms

## [react-hook-form](https://react-hook-form.com/get-started)

Inputs must have unique name

```react
import React from 'react'
import { useForm } from 'react-hook-form'

export default function App() {
  const { register, handleSubmit, errors } = useForm()
  const onSubmit = data => { console.log(data) }

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input name="example" defaultValue="test" ref={register} />
      <input name="exampleRequired" ref={register({ required: true })} />
      {errors.exampleRequired && <span>This field is required</span>}
      <input type="submit" />
    </form>
  )
}
```

List of validation rules supported by:

- required
- min
- max
- minLength
- maxLength
- pattern
- validate

## Inputs

```js
  const [title, setTitle] = useState("Enter Title...");

	//........

	<input
    className="border-none bg-transparent outline-none"
    value={title}
    onChange={e => setTitle(e.target.value)}
  />
```



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
  }

  handleInputChange = (event) =>  { 
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    
    this.setState({
      [target.name]: value //es6 computed property syntax
    });
  }
  
  handleSubmit(event) {
    event.preventDefault();
    //.. process submission with state
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
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