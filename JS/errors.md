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
} finally { //can just have the finally if you dont want to catch error?
  //do something regardless of result
}
```

Error has name, message and can have custom info/code

*could technically throw and catch anything*

## Custom Errors

```js
export class MediaError extends Error {
  //without constructor will include this class in stack trace
  constructor(message, user_message, err) {
    super(message);
    this.name = "MediaError";
    this.user_message = user_message;
    if (Error.captureStackTrace !== undefined) {
      //Firefox problem, since its non-standard
      Error.captureStackTrace(this, MediaError);
    }
  }
}
```

#### Common Custom Errors

##### Axios

err.response

#### HTTP

Check out http-errors Node package or HTTP Fundamentals

