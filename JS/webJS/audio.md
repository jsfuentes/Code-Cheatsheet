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

## Audio Viz

```js
useEffect(() => {
  let analyser; //"global"

  function update() {
    // Schedule the next update
    if (analyser) {
      requestAnimationFrame(update);

      const frequencyData = new Uint8Array(analyser.frequencyBinCount);
      const els = document.querySelectorAll(".audio_bar");
      // Get the new frequency data
      analyser.getByteFrequencyData(frequencyData);
      els.forEach((el, i) => {
        const newPercent = (frequencyData[i] / 255) * 100;
        el.style.height = newPercent + "%";
      });
      // const sumOfData = frequencyData.reduce((l, c) => l + c);
      // const max = analyser.frequencyBinCount * 255;
      // const percentOfMax = (sumOfData / max) * 100;
      // // el.style.height = percentOfMax + "%";
    }
  }

  if (audioStream && recordingState === RECORDING_STATE) {
    console.log("Creating contexts");
    const audioCtx = new AudioContext();
    const source = audioCtx.createMediaStreamSource(audioStream);
    analyser = audioCtx.createAnalyser();
    source.connect(analyser);
    analyser.fftSize = 2048;
    // analyser.connect(audioCtx.destination);
    update();
    return () => (analyser = null);
  }
}, [audioStream, recordingState]);

function bars() {
  const barCount = 2048 / 2;
  const percentPer = (1 / barCount) * 100;
  console.log(percentPer);
  let myBars = [];
  for (let i = 0; i < barCount; i++) {
    myBars.push(
      <div
      key={i}
  className="absolute audio_bar bg-pink-500"
  style={{ width: percentPer + "%", left: i * percentPer + "%" }}
/>
);
}
return myBars;
}
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

