# Regex

See regex under / for regex details

## Create Object

```js
var re = /pattern/flags;
var re = /ab+c/;
```

## Flags

| Flag | Description                                                  |
| ---- | ------------------------------------------------------------ |
| `g`  | Global search.                                               |
| i    | Case-insensitive search.                                     |
| m    | Multi-line search.                                           |
| u    | unicode; treat a pattern as a sequence of unicode code points |
| y    | Perform a "sticky" search that matches starting at the current position in the target string. See [`sticky`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/sticky) |

## Functions

Array of info: ["(AERO ST)", index: 18, input: "Aerospace Studies (AERO ST)", groups: undefined]; 

| Method                                                       | Description                                                  |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`exec`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) | `RegExp` method, search for match,  return array of info or null | var myRe = /d(b+)d/g; var myArray = myRe.exec('cdbbdbsbz');  |
| [`test`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test) | `RegExp` method, check for match, returns true or false      |                                                              |
| [`match`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match) | `String` method, search for a match, returns an array of info or null | "Aerospace Studies (AERO ST)".match(/\(.*\)/) => ["(AERO ST)", index: 18, input: "Aerospace Studies (AERO ST)", groups: undefined] |
| [`search`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/search) | `String` method, that tests for a match in a string. It returns the index of the match, or -1 if the search fails. |                                                              |
| [`replace`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace) | A `String` method that executes a search for a match in a string, and replaces the matched substring with a replacement substring. |                                                              |
| [`split`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) | A `String` method that uses a regular expression or a fixed string to break a string into an array of substrings. |                                                              |