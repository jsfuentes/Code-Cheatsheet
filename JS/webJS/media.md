# Media

## Getting Streams

#### Get Camera

```javascript
function recordCamera() {
  function getCameraStream(stream) {
    console.log("Starting Camera");
    stream.onended = () => {
      console.log("Camera Stream ended.");
    };
    setCamStream(stream);
  }

  navigator.webkitGetUserMedia(
    {
      audio: false,
      video: {
        mandatory: { minWidth: 1280, minHeight: 720 }
      }
    },
    getCameraStream,
    getUserMediaError
  );
}
```

#### Get Audio

Do it seperate then add as a track to your stream, might be able to just say audio true, but mac makes it jank or something idk

```javascript
navigator.webkitGetUserMedia(
  { audio: true, video: false },
  getAudio,
  getUserMediaError
);
```

## Using Stream

#### Play Video of MediaStream

```jsx
  const vRef = useRef(null);
  
	if (camStream) vRef.current.srcObject = camStream;

  return (<video
      className="h-full scale-medium"
      muted
      autoPlay
      data-setup="{}"
      ref={vRef}
      />)
```

#### Record

```javascript
let audioStream;
let numRecordedChunks = 0;
let recordedChunks = [];
let recorder;

const recorderOnDataAvailable = event => {
  console.log("Data available");
  if (event.data && event.data.size > 0) {
    recordedChunks.push(event.data);
    numRecordedChunks += event.data.byteLength;
  }
};


const getMediaStream = stream => {
  stream.onended = () => {
    console.log("Media stream ended.");
  };

  if (audioStream !== null) {
    console.log("Adding audio track.");
    let audioTracks = audioStream.getAudioTracks();
    stream.addTrack(audioTracks[0]);
  }

  try {
    console.log("Start recording the stream.");
    recorder = new MediaRecorder(stream, { mimeType: "video/webm" });
  } catch (e) {
    console.assert(false, "Exception while creating MediaRecorder: " + e);
    return;
  }

  recorder.ondataavailable = recorderOnDataAvailable;
  recorder.onstop = () => {
    console.log("recorderOnStop fired");
  };
  recorder.start();
  console.log("Recorder is started.");
};
```

Actually then using that recording

```jsx
const play = () => {
  const blob = new Blob(recordedChunks, { type: recordedChunks[0].type });
  const blobURL = URL.createObjectURL(blob);
  let currentRecording = (blobURL);
  console.log(recordedChunks, blob, blobURL);
};

return (
  <video 
  	controls autoPlay 
  	data-setup="{}" src={currentRecording} 
	/>);
```

This sends it to transloadit, but you can also use the base uppy to send straight to S3

```javascript
import Robodog from "@uppy/robodog";

function send() {
  const blob = new Blob(recordedChunks, { type: recordedChunks[0].type });
	
  const resultPromise = Robodog.upload([blob], {
    params: {
      auth: { key: "352f4e9e50f84a4591c9f2039571cbc5" },
      template_id: "ad391eea34034ef28e04e8ad1a024b14"
    }
  });
  resultPromise
    .then(bundle => {
    console.log("TRANSLOAD it success");
    console.log(bundle.transloadit);
    console.log(bundle.results); 
  })
    .catch(err => console.error("Transerr", err));
}
```

