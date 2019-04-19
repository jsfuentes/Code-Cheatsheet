# AJAX
Asynchronous Javascript And XML

## Fetch

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

## Fundamentals

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

## Parse JSON Response
Could also get XML, but nahhhhh
`JSON.parse(http.responseText);`
JSON.parse is only avaliable in most modern browsers, could use lib like jQueryd

## Trigger in Dom
Events like onclick

## XMLHttpRequest States
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

## Submitting Forms

```js
document.myform.onsubmit = function() {
  //ajax call
  return false; //stops form from submitting regularly
}
```

