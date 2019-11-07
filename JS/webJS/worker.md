# [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)

Run js files in background threads without blocking UI

Communicate with JS code that called it with messages

## Dedicated Worker

Only accessible by script that called it

main.js

```js
const myWorker = new Worker('worker.js');
//In React: 
//import jsxWorker from "../worker/jsx.js";
//const myWorker = new Worker(jsxWorker);

first.onchange = function() {
  myWorker.gs
  ([first.value,second.value]);
  console.log('Message posted to worker');
}

second.onchange = function() {
  myWorker.postMessage([first.value,second.value]);
  console.log('Message posted to worker');
}

myWorker.onmessage = function(e) {
  result.textContent = e.data;
  console.log('Message received from worker');
}
```

worker.js

```js
//In React:
//export default () => {

importScripts('foo.js', 'bar.js'); //synchronous
importScripts('//example.com/hello.js');

if (window.Worker) {
  onmessage = function(e) {
    console.log('Message received from main script');
    var workerResult = 'Result: ' + (e.data[0] * e.data[1]);
    console.log('Posting message back to main script');
    postMessage(workerResult);
  }
}

//}
```

### Using in React

Can use web pack

webpack.config.js

```js
    module: {
      strictExportPresence: true,
      rules: [
        //.....
            {
              test: /\.worker\.js$/,
              include: paths.appSrc,
              use: { loader: "worker-loader" }
            },
        //.......
```

component.js

```js
import JSXWorker from "./jsx.worker";

// console.log("Creating JSX Worker");
const worker = new JSXWorker();

worker.addEventListener("message", ({ data }) => {
```

## More

```js
myWorker.terminate();
```

Handle errors with `onerror` event handler

Workers can spawn more workers yay

## Shared Worker

Accessible by multiple scripts

Use port instead of messages to communicate

## Service Worker

Service Workers offer a lot more functionality for creating Progressive Web Apps which give a great experience for offline users or users with slow internet connections. The Service Worker can be used as a proxy for network events, allowing us to cache resources for offline use.