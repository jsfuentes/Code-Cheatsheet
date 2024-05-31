# Flask-SQLAlchemy

```bash
pip install -U Flask-SQLAlchemy
```

#### Config

Urls accepted:

- `postgresql://postgres:CCCCCC-rujjiw-5fudti@database-1.CCCCC4egs9fm.us-east-2.rds.amazonaws.com:5432`

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

# create the extension
db = SQLAlchemy()
# create the app
app = Flask(__name__)
# configure the SQLite database, relative to the app instance folder
app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///project.db"
# initialize the app with the extension
db.init_app(app)
```

Create tables

```python
with app.app_context():
    db.create_all()
```

*or use flask-migrate*

## Creates a new session for each request

```python
@app.route("/users")
def user_list():
    users = db.session.execute(db.select(User).order_by(User.username)).scalars()
    return render_template("user/list.html", users=users)
```

