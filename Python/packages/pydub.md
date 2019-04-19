# Pydub

Manipulate Audio

## Split

```python
from pydub import AudioSegment
sound = AudioSegment.from_file("./Community.mp3")

halfway_point = len(sound) // 2
print(len(sound))
first_half = sound[:halfway_point]

# create a new file "first_half.mp3":
first_half.export("./Com.mp3", format="mp3")
```

## Access Raw Data

```python
AudioSegment(...).raw_data
```

