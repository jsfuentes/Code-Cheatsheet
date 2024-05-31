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

```bash
flask run --debug #to run in debug mode
flask run -h 0.0.0.0 -p 80 --debug # to set url
```

*Default of 5000 can cause problems on Mac cuz 5000 is used for control center*

### Flask CLI

```python
# Run `flask createdb` to run this
@app.cli.command()
def createdb():
  # import logging
  # logging.basicConfig()
	# logging.getLogger('sqlalchemy.engine').setLevel(logging.INFO)

  from app.models.user import User
  from app.models.question import Question
  print("Created DBBBB")
  db.create_all()
```

