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

