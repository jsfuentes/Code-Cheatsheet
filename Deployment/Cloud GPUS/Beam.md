# [Beam](https://beam.cloud)

Deploy gpu

Minimum 3.7

```bash
pip install beam-sdk
beam start app.py
```

app.py

```python
import beam

# The environment the app will run in
app = beam.App(
    name="mowgli-wav2lip",
    cpu=4,
    memory="16Gi",
    python_version="python3.7",
    python_packages="requirements.txt",
    commands=["apt-get update && apt-get install -y ffmpeg"],
)


# # A trigger that sets the app to run on a schedule
# app.Trigger.Schedule(
#     # The frequency can be denoted in cron or every syntax
#     when="every 5m",
#     # The handler is the function that will run when the task is invoked
#     handler="run.py:process_images",
# )

app.Trigger.RestAPI(
    inputs={"video_url": beam.Types.String()},
    outputs={"pred": beam.Types.String()},
    handler="run.py:transcribe",
)

app.Mount.PersistentVolume(
    path="./trained_models",
    name="trained_models"
)
```

## Volume

```
python Wav2Lip/inference.py --checkpoint_path trained_models/Wav2Lip/wave2lip_gan.pth --face trained_models/Wav2Lip/video.mp4 --audio trained_models/Wav2Lip/audio.mp3 --outfile trained_models/Wav2Lip/result.mp4
```