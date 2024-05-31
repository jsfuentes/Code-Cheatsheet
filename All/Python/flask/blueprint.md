# Blueprint

Split up your app routes into separate files and register them at like `/api/v1`

## Creation

simplepage.py

```python
from flask import Blueprint

simple_page = Blueprint('simple_page', __name__,
                        template_folder='templates') #can leave template_folders out

@simple_page.route('/')
def index():
  return render_template("hello.html")
```

## Registering

app.py

```python
from yourapplication.simple_page import simple_page

app = Flask(__name__)
app.register_blueprint(simple_page)

app.register_blueprint(user, url_prefix='/user')
```

## Linking
url_for('admin.index')
