# Flask

## Most basic

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'
```

## FLASH
```python
From flask import flash
@app.route('/login', methods=['GET', 'POST'])
def login():
	…..
flash('You were successfully logged in')
```
