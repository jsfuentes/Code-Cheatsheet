# Flask

## Most basic

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'
```

### Flask Run

Flask run finds trys to find right file to run and loads .env too 

`flask run -h 0.0.0.0 -p 80`

