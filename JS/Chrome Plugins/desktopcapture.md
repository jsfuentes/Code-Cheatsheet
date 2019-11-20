# Desktop Capture

Permission

Half implemented solution, good luck

Uses WebRTC by using navigator.mediaDevices

```js
async function getMedia(streamId) {
  let stream = null;

  try {
    navigator.mediaDevices
      .getUserMedia({
        video: {
          mandatory: {
            chromeMediaSource: "desktop",
            chromeMediaSourceId: streamId
          }
        }
      })
      .then(returnedStream => {
        stream = returnedStream;
        const video = document.querySelector("#video");
        video.src = window.URL.createObjectURL(stream);//wasnt working at time, but maybe
      })
      .catch(err => {
        console.error("Could not get stream: ", err);
      });

    /* use the stream */
  } catch (err) {
    debug("navigator", err);
    /* handle the error */
  }
}

function captureDesktop() {
  browser.desktopCapture.chooseDesktopMedia(
    ["screen", "audio"],
    (streamId, options) => {
      getMedia(streamId);
    }
  );
}

captureDesktop();
```

