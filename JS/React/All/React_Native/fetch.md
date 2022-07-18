# Networking

- Implementation of XMLHttpRequestAPI means **axios** works!

- Also [Fetch API]
- iOS requires https unless you add an [expection](https://facebook.github.io/react-native/docs/integration-with-existing-apps#test-your-integration)
- Cookie authentication is currently [unstable](https://github.com/facebook/react-native/issues/23185)

```jsx
fetch('https://mywebsite.com/mydata.json');

fetch('https://mywebsite.com/endpoint/', {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    firstParam: 'yourValue',
    secondParam: 'yourOtherValue',
  }),
});

async function getMoviesFromApi() {
  try {
    let response = await fetch(
      'https://facebook.github.io/react-native/movies.json',
    );
    let responseJson = await response.json();
    return responseJson.movies;
  } catch (error) {
    console.error(error);
  }
}
```

## Websockets

Full-deplex communication channels over a single TCP connection

```jsx
const ws = new WebSocket('ws://host.com/path');

ws.onopen = () => {
  // connection opened
  ws.send('something'); // send a message
};

ws.onmessage = (e) => {
  // a message was received
  console.log(e.data);
};

ws.onerror = (e) => {
  // an error occurred
  console.log(e.message);
};

ws.onclose = (e) => {
  // connection closed
  console.log(e.code, e.reason);
};
```

