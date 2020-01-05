# Config

With nothing special, you use Ajax 

```javascript
fetch(chrome.extension.getURL('./config.json'))
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

Or you can just use a bundler that uses imports

Or you could make a promise, then use ran all your code in the callback

