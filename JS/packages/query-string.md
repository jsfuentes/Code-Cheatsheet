# Query-string

```js
import queryString from 'query-string'

//.......(props) {
const vals = queryString.parse(props.location.search); 
// "?filter=top&origin=im"
console.log(vals.filter); // "top"
console.log(vals.origin); // "im"

const stringified = queryString.stringify(parsed);
```

