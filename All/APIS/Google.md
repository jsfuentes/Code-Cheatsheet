# Google APIS

## User Auth

#### [On the Web](https://developers.google.com/identity/sign-in/web/sign-in)

#### On the Backend

#### Setup

1) Go to https://console.developers.google.com/

2) Create/Select a Project

3) In Credientals tab, create an OAuth

4) Add `localhost:<port>` and `localhost` to get it to work 

#### Usage

Get the id_token, request the scopes `profile` and `email`

Then you can get profile info at `https://www.googleapis.com/oauth2/v1/userinfo?alt=json&access_token=[accesstoken]`

## API Auth

Can download their file and do some gcloud command to get token 

Or can create API KEY then attach to urls with `?key=[APIKEY]`

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

## Image to Object Labels

https://cloud.google.com/vision/docs/features-list

```
body = {
  "requests": [
    {
      "image": {
        "source": {
          "imageUri": "https://www.vet.cornell.edu/sites/default/files/Dog%20running%20in%20field.png"
        }
      },
      "features": [
        {
          "type": "LABEL_DETECTION",
          "maxResults": 1
        },
        {
          "type": "FACE_DETECTION",
          "maxResults": 3
        }
      ]
    }
  ]
}
header = "Content-Type: application/json; charset=utf-8"
url = https://vision.googleapis.com/v1/images:annotate?key=[API_KEY]
```

## Text to Speech

```
body = {
  "input":{
    "text":"Android is a mobile operating system developed by Google, based on the Linux kernel and designed primarily for touchscreen mobile devices such as smartphones and tablets."
  },
  "voice":{
    "languageCode":"en-gb",
    "name":"en-GB-Standard-A",
    "ssmlGender":"FEMALE"
  },
  "audioConfig":{
    "audioEncoding":"MP3"
  }
}

url = https://texttospeech.googleapis.com/v1/text:synthesize?key=[API_KEY]
```

