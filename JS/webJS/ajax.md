# AJAX
Asynchronous Javascript And XML

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
