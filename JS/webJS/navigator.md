# Navigator

Interact with media devices and more

**See media for getting and recording media**

**If the user blocks the browser request, you won’t be able to ask for the permission again.** On the contrary, if the user dismisses your custom request

#### Find Devices

```javascript
navigator.mediaDevices.enumerateDevices().then(devices => {
  const audioInputs = devices.filter(d => d.kind === "audioinput");
  if (audioInputs.length === 0) console.error("No audio input devices");
});
```

Devices Output

- .kind => `audioinput` | `videoinput` | `audiooutput` 

```js
[{"deviceId":"default","kind":"audioinput","label":"Default - Internal Microphone (Built-in)","groupId":"fb2d9c14fbd30628d3fd7fe2b5dc62880dc4684ac956b68db7b9ecca88c1405b"},{"deviceId":"459560c107d13f6c86e1d8afcb97163f893c0c97dfed4d1921bfd2e12c6fbb7f","kind":"audioinput","label":"Internal Microphone (Built-in)","groupId":"fb2d9c14fbd30628d3fd7fe2b5dc62880dc4684ac956b68db7b9ecca88c1405b"}, //.... ]
```

```js
  const constraints = {
    audio: {
      //if doesnt exist, then OverconstrainedError
      deviceId: {exact: selectedAudio.deviceId}
    },
    video: {
      deviceId: {exact:  selectedVideo.deviceId}
    }
  };

  navigator.mediaDevices.getUserMedia(constraints).
    then(gotStream).catch(handleError);
```

#### Permissions

- .state => `denied` | `granted` | `prompt`

```js
navigator.permissions.query({ name: "microphone" }).then(p => {
  console.log(p.state);
});
navigator.permissions.query({ name: "microphone" }).then(console.log);
```

