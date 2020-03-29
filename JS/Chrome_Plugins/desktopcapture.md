# Desktop Capture

Permission: `desktopCapture`

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

### Getting Audio

GetUserMedia for audio, can't request permissions in background or popup page, must request in the content script. Then send message to background, so that it succeeds.

https://stackoverflow.com/questions/50991321/chrome-extension-getusermedia-throws-notallowederror-failed-due-to-shutdown

*Don't forget to allow="camera, microhpone" as iframe attribute*

No interest in allowing get user media from extension pages(background/popup) => https://bugs.chromium.org/p/chromium/issues/detail?id=1006742

