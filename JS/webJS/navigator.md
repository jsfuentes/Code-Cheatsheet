# Navigator

**See media for more**

Interact with media devices and more

```javascript
navigator.mediaDevices.enumerateDevices().then(devices => {
  const audioInputs = devices.filter(d => d.kind === "audioinput");
  if (audioInputs.length === 0) console.error("No audio input devices");
});

navigator.permissions.query({ name: "microphone" }).then(console.log);
```

## Record Audio

JS

```javascript
const stopButton = document.getElementById("stop");

const handleSuccess = function(stream) {
  console.log("Success");
  const options = { mimeType: "audio/webm" };
  const mediaRecorder = new MediaRecorder(stream, options);

  stopButton.onclick = () => {
    mediaRecorder.stop();
  };

  mediaRecorder.addEventListener("dataavailable", function(e) {
    if (e.data.size > 0) {
      console.log("Stopped", e);
      const audioURL = URL.createObjectURL(e.data);
      downloadLink.href = audioURL;
      downloadLink.download = "help.webm";
      if (window.URL) {
      	player.srcObject = stream;
    	} else {
     		player.src = stream;
    	}
    }
  });

  mediaRecorder.start();
};

navigator.mediaDevices
  .getUserMedia({ audio: true, video: false })
  .then(handleSuccess);
```

Html

```html
<a id="download"> Download </a>
<button id="stop"> Stop </button>
<audio id="player" controls></audio>
```

