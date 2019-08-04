# JSON

COmments not supported

```json
{ 
  "telephone": {
    "comment": "The phone number associated with this POI.",
    "type": "string",
    "example": "(415)383-9600"
  },
  "timezone": {
    "comment": "The IANA timezone this POI is located in.",
    "type": "string",
    "example": "America/Los_Angeles"
  },
}
```

## Parsing

```js
var obj = JSON.parse('{ "name":"John", "age":30, "city":"New York"}');
let myJSON = JSON.stringify(obj);
```



