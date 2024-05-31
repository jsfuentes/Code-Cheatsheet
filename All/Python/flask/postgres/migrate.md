# Flask-Migrate

```bash
pip install Flask-Migrate
```

Migrations are handle by `flask-migrate/alembic`

Creates folder for migrations 

## Setup

```python
# extensions.py
from flask_migrate import Migrate

migrate = Migrate()

# app.py
from app.extensions import migrate

#......
migrate.init_app(app, db)
```

Then run this to create the db tables

```bash
flask db init
flask db migrate -m "Message goes here I think"
flask db upgrade
```

## Generate New Migration Files

```bash
flask db migrate -m "Message goes here I think"
flask db upgrade
```
