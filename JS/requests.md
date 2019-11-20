# Making a request

Several Options:

- axios
- requests
- fetch
- raw XMLhttprequest
- jquery

## Axios

Promise based HTTP client, best

```js
const axios = require('axios');
import axios from 'axios';

//GET
axios.get("/event", { params: { api_key })
  .then(response => {
    console.log(response.data.url);
    console.log(response.data.explanation);
  })
  .catch(error => {
    console.log(error);
  });

//POST
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

**axios.get(url[, config])**

**axios.post(url[, data[, config]])**

Multiple Requests

```js
axios.all([
  axios.get('https://api.nasa.gov/planetary/apod?api_key=DEMO_KEY&date=2017-08-03'),
  axios.get('https://api.nasa.gov/planetary/apod?api_key=DEMO_KEY&date=2017-08-02')
]).then(axios.spread((response1, response2) => {
  console.log(response1.data.url);
  console.log(response2.data.url);
})).catch(error => {
  console.log(error);
});
```

## Requests

Simplified version of python 

```js
const request = require('request');

request('https://api.nasa.gov/planetary/apod?api_key=DEMO_KEY', { json: true }, (err, res, body) => {
  if (err) { return console.log(err); }
  console.log(body.url);
  console.log(body.explanation);
});
```

## Fetch

Builtin to modern browsers, adds parse step compared to axios and some other gotchas

```js
fetch('./api/some.json')
  .then(
    function(response) {
      if (response.status !== 200) {
        console.log('Looks like there was a problem. Status Code: ' +
          response.status);
        return;
      }

      // Examine the text in the response
      response.json().then(function(data) {
        console.log(data);
      });
    }
  )
  .catch(function(err) {
    console.log('Fetch Error :-S', err);
  });
```

Response.status

.json()

.text()

#### Advanced Fetch

```javascript
fetch(url, {
        method: "POST", // *GET, POST, PUT, DELETE, etc.
        mode: "cors", // no-cors, cors, *same-origin
        cache: "no-cache", // *default, no-cache, reload, force-cache, only-if-cached
        credentials: "same-origin", // include, *same-origin, omit
        headers: {
            "Content-Type": "application/json",
            // "Content-Type": "application/x-www-form-urlencoded",
        },
        redirect: "follow", // manual, *follow, error
        referrer: "no-referrer", // no-referrer, *client
        body: JSON.stringify(data), // body data type must match "Content-Type" header
    })
    .then(response => response.json());
```

#### Async await

```js
const response = await fetch('https://api.com/values/1');
const json = await response.json();
console.log(json);
```

#### Creating URL Queries

```javascript
function encodeQueryData(data) {
   const ret = [];
   for (let d in data)
     ret.push(encodeURIComponent(d) + '=' + encodeURIComponent(data[d]));
   return ret.join('&');
}
```

## OG Fundamental

```js
var http = new XMLHttpRequest();
http.open("GET", "url", true); //true if we want it to be synchronous
http.send();
http.onreadystatechange = function() {
  if(http.readyState == 4 && http.status == 200) {
    //...........
    //usually update DOM somehow
  }
}
```

#### Parse JSON Response

Could also send and receive XML, but nahhhhh
`JSON.parse(http.responseText);`
JSON.parse is only avaliable in most modern browsers, could use lib like jQuery

#### XMLHttpRequest States

- 0 request not initialized
- 1 request set up
- 2 request has been sent
- 3 request is in process
- 4 request is complete //essential

## In JQuery
```js
$.get("url", function(data) {
  .....
});
```
