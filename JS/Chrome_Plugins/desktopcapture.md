# Desktop Capture

Permission: `desktopCapture`

Uses WebRTC by using navigator.mediaDevices

```js
startStreams() {
    return new Promise((resolve, reject) => {
      if (this.displayStream) {
        //idempotentic
        resolve();
        return;
      }

      async function desktopCallback(streamId, options) {
        if (!streamId) {
          debug("Cancelled");
          resolve();
          return;
        }

        try {
          const stream = await navigator.mediaDevices.getUserMedia({
            video: {
              mandatory: {
                chromeMediaSource: "desktop",
                chromeMediaSourceId: streamId
              }
            },
            audio: false
          });
          debug("Started display stream");
          this.displayStream = stream;
        } catch (err) {
          await browser.storage.sync.set({ [C.curFilename]: null });
          debug("Getting the screen recording failed");
          Sentry.captureException(err);
          console.error(err);
          reject(err);
          return;
        }

        await this.startAudio(); //try to get audio

        if (this.audioStream) {
          const audioTracks = this.audioStream.getAudioTracks();
          if (this.displayStream) {
            this.displayStream.addTrack(audioTracks[0]);
          } else {
            //stop audio if no displayStream(user denied)
            audioTracks.forEach(t => t.stop());
          }
        }

        resolve();
      }
      desktopCallback = desktopCallback.bind(this);

      browser.desktopCapture.chooseDesktopMedia(
        ["screen", "audio"],
        desktopCallback
      );
    });
  }
```

### Getting Audio

GetUserMedia for audio, can't request permissions in background or popup page, must request in the content script. Then send message to background, so that it succeeds.

https://stackoverflow.com/questions/50991321/chrome-extension-getusermedia-throws-notallowederror-failed-due-to-shutdown

*Don't forget to allow="camera, microhpone" as iframe attribute*

No interest in allowing get user media from extension pages(background/popup) => https://bugs.chromium.org/p/chromium/issues/detail?id=1006742

