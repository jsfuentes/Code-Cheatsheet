# Blueprint

It’s a set of operations which can be registered on an application allowing:
- Register set of routes at prefix `api/v1`
- Split up app

## Creation
```python
simple_page = Blueprint('simple_page', __name__,
                        template_folder='templates')

@simple_page.route('/')
def index():
  return render_template("hello.html")
```

## Registering
```python
from yourapplication.simple_page import simple_page

app = Flask(__name__)
app.register_blueprint(simple_page)

app.register_blueprint(user, url_prefix='/user')
```

## Linking
url_for('admin.index')
