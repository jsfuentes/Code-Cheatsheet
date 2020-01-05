# Errors

```
new Error([message[, fileName[, lineNumber]]])
```

- Filename and LineNumber default
- .name is Error default but there are [more](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error) 
- .stack is call stack that most envs give

*New and just `Error` are same*

## Usage

```javascript
try {
  throw new Error("Parameter is not a number!");
  //throw new Error([message[, fileName[, lineNumber]]])
}
catch(err) {
    alert(e.message); // This is an error
}
```

Error has name, message and can have custom info/code

*could technically throw and catch anything*

## Custom Errors

```js
class GoodError extends Error {
  //without constructor will include this class in stack trace
    constructor(...args) {
        super(...args)
        Error.captureStackTrace(this, GoodError)
      this.data = "hi";
    }
}
```



#### Common Custom Errors

##### Axios

err.response

#### HTTP

Check out http-errors Node package or HTTP Fundamentals

