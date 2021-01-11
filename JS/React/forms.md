# Forms

## [react-hook-form](https://react-hook-form.com/get-started)

[Form Builder](https://react-hook-form.com/form-builder/)

Inputs must have unique name

```jsx
import React from "react";
import { useForm } from "react-hook-form";

export default function App() {
  const { register, handleSubmit, errors } = useForm();
  function onSubmit(data) { console.log(data); }

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input name="example" defaultValue="test" ref={register} />
      <input name="exampleRequired" ref={register({ required: true })} />
      {errors.exampleRequired && <span>This field is required</span>}
      <button type="submit" > Submit </button>
    </form>
  );
}
```

List of validation rules supported: required | min | max | minLength | maxLength | pattern | validate (custom function)

## TextInput

```react
TextInput.propTypes = {
  title: PropTypes.string,
  name: PropTypes.string.isRequired,
  registerInForm: PropTypes.any.isRequired,
  placeholder: PropTypes.string,
  errors: PropTypes.object,
  className: PropTypes.string,
};

export function TextInput(props) {
  const {
    title,
    placeholder,
    name,
    registerInForm,
    errors,
    className,
  } = props;

  return (
    <div className={className}>
      {title && (
        <label
          htmlFor={name} //use randomid if multiple per page
          className="block font-medium leading-5 text-gray-600"
        >
          {title}
        </label>
      )}
      <div className="mt-2">
        <input
          type="text"
          id={name}
          className={
            "form-input block w-full transition duration-150 ease-in-out " +
            (className ? `${className}` : +"")
          }
          name={name}
          placeholder={placeholder}
          ref={registerInForm}
        />
        {errors && errors[name] && (
          <div className="mt-1 text-red-500">
            {generateErrorMessage(errors, name)}
          </div>
        )}
      </div>
    </div>
  );
}

function generateErrorMessage(errors, key) {
  const type = errors[key].type;
  switch (type) {
    case "maxLength":
      return "This field is too long";
    case "required":
      return "Oops, you missed this field";
    default:
      return "Invalid value";
  }
}
```

## Controlled Components

Normally form elements such as `<input> `  maintain their own state and update based on input. To combine with React state, let React state be the “single source of truth” by updating it on change

- React normalizes different tags like select, textarea, and text to have value attribute

```jsx
export default function Create() {
  const [name, setName] = useState("");
  const [noEvent, setNoEvent] = useState(true);

  function onSubmit(event) {
    event.preventDefault();
    axios
      .post("/api/events", { name, noEvent })
      .then((resp) => debug("resp recieved", resp));
  }

  return (
    <form
      className="border-4 border-solid rounded-sm flex flex-col justify-center items-center p-6 mb-4"
      onSubmit={onSubmit}
    >
      <div className="text-3xl font-bold">Create Event</div>
      <label
        className="block text-gray-700 text-sm font-bold mb-2"
        htmlFor="name"
      >
        Name
      </label>
      <input
        className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        id="name"
        type="text"
        placeholder="Event Title"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <label
        className="block text-gray-700 text-sm font-bold mb-2"
        htmlFor="noEvent"
      >
        noEvent
      </label>
      <input
        id="noEvent"
        type="checkbox"
        checked={noEvent}
        onChange={(e) => setNoEvent(e.target.checked)}
      />
      <button
        className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        type="submit"
      >
        Create
      </button>
    </form>
  );
}
```

## Custom Hooks

```jsx
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

```jsx
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