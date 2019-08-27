# Proptypes

Typechecking only in development, only gives a console warning

To run typechecking on the props for a component, you can assign the special `propTypes` property:

```react
import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};
```

### Default Values

```js
// Specifies the default values for props:
Greeting.defaultProps = {
  name: 'Stranger'
};
//with transform-class-properties babel transform
class Greeting extends React.Component {
  static defaultProps = {
    name: 'stranger'
  }

  render() {
    return (
      <div>Hello, {this.props.name}</div>
    )
  }
}
```

### All Types

By default all are optional

```js
MyComponent.propTypes = {
  // Native types
  optionalArray: PropTypes.array,
  optionalBool: PropTypes.bool,
  optionalFunc: PropTypes.func,
  optionalNumber: PropTypes.number,
  optionalObject: PropTypes.object,
  optionalString: PropTypes.string,
  optionalSymbol: PropTypes.symbol,
  // Add `isRequired` to any
  requiredFunc: PropTypes.func.isRequired,
  // A React element.
  optionalElement: PropTypes.element,
  // A React element type (ie. MyComponent).
  optionalElementType: PropTypes.elementType,
  // Anything that can be rendered: numbers, strings, elements or an array(or fragment) containing these types.
  optionalNode: PropTypes.node,
  // declare prop is an instance of a class using instanceof 
  optionalMessage: PropTypes.instanceOf(Message),
  // Limit to specific values with enum
  optionalEnum: PropTypes.oneOf(['News', 'Photos']),
  // An object that could be one of many types
  optionalUnion: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Message)
  ]),
  // An array of a certain type
  optionalArrayOf: PropTypes.arrayOf(PropTypes.number),
  // An object with property values of a certain type
  optionalObjectOf: PropTypes.objectOf(PropTypes.number),
  // An object taking on a particular shape
  optionalObjectWithShape: PropTypes.shape({
    color: PropTypes.string,
    fontSize: PropTypes.number
  }),
  // An object with warnings on extra properties
  optionalObjectWithStrictShape: PropTypes.exact({
    name: PropTypes.string,
    quantity: PropTypes.number
  }),   
  // A value of any data type
  requiredAny: PropTypes.any.isRequired,
  // You can also specify a custom validator. It should return an Error object if the validation fails. Don't `console.warn` or throw, as this won't work inside `oneOfType`.
  customProp: function(props, propName, componentName) {
    if (!/matchme/.test(props[propName])) {
      return new Error(
        'Invalid prop `' + propName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  },
  // You can also supply a custom validator to `arrayOf` and `objectOf`.
  // It should return an Error object if the validation fails. The validator
  // will be called for each key in the array or object. The first two
  // arguments of the validator are the array or object itself, and the
  // current item's key.
  customArrayProp: PropTypes.arrayOf(function(propValue, key, componentName, location, propFullName) {
    if (!/matchme/.test(propValue[key])) {
      return new Error(
        'Invalid prop `' + propFullName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  })
};

```

