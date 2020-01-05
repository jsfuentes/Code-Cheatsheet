# AudioContext

Create, manipulate, and play audio

If you dont want to play it, use [`OfflineAudioContext`](https://developer.mozilla.org/en-US/docs/Web/API/OfflineAudioContext).

```javascript
const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
const sine = audioCtx.createOscillator();
sine.start();
sine.connect(audioCtx.destination);
```

## Simple

1. Create the audio context.
2. Inside the context, create sources — such as [``](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio), oscillator, or stream.
3. Create effects nodes, such as reverb, biquad filter, panner, or compressor.
4. Choose the final destination for the audio, such as the user's computer speakers.
5. Establish connections from the audio sources through zero or more effects, eventually ending at the chosen destination.

