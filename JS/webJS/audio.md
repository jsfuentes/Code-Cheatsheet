# Audio

## Play Audio

```js
const audio = new Audio('audio_file.mp3'); //or url
audio.play();
audio.pause();
```

```js
audio.currentTime;
audio.duration;
audioPlayer.addEventListener("timeupdate", () => {})
audioPlayer.addEventListener("ended", () => {});
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

## Create Audio

Create, manipulate, and play audio

If you dont want to play it, use [`OfflineAudioContext`](https://developer.mozilla.org/en-US/docs/Web/API/OfflineAudioContext).

```javascript
const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
const sine = audioCtx.createOscillator();
sine.start();
sine.connect(audioCtx.destination);
```

1. Create the audio context.
2. Inside the context, create sources — such as [``](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio), oscillator, or stream.
3. Create effects nodes, such as reverb, biquad filter, panner, or compressor.
4. Choose the final destination for the audio, such as the user's computer speakers.
5. Establish connections from the audio sources through zero or more effects, eventually ending at the chosen destination.

