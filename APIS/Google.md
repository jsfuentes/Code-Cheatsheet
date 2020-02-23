# Google APIS

## Auth

#### [On the Web](https://developers.google.com/identity/sign-in/web/sign-in)

#### On the Backend

#### Setup

1) Go to https://console.developers.google.com/

2) Create/Select a Project

3) In Credientals tab, create an OAuth 

#### Usage

Get the id_token, request the scopes `profile` and `email`

Then you can get profile info at `https://www.googleapis.com/oauth2/v1/userinfo?alt=json&access_token=[accesstoken]`

## Speech to Text

Credientials determined automatically if you set the environment variable GOOGLE_APPLICATION_CREDENTIALS to the file path of the Google JSON file

```python
import io
import os

# Imports the Google Cloud client library
from google.cloud import speech
from google.cloud.speech import enums
from google.cloud.speech import types

# Instantiates a client
client = speech.SpeechClient()

# The name of the audio file to transcribe
file_name = "./Endgame.mp3"

# Loads the audio into memory
with io.open(file_name, 'rb') as audio_file:
    content = audio_file.read()
    audio = types.RecognitionAudio(content=content)

config = types.RecognitionConfig(
    encoding=enums.RecognitionConfig.AudioEncoding.LINEAR16,
    sample_rate_hertz=16000,
    language_code='en-US',
    enableWordTimeOffsets=True)

# Detects speech in the audio file
response = client.LongRunningRecognize(config, audio)

for result in response.results:
    print('Transcript: {}'.format(result.alternatives[0].transcript))
```

