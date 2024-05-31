# Config

```python
import os
import json


class Config:
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'hard to guess secret'
    # Specific name for flask-sqlalchemy
    SQLALCHEMY_DATABASE_URI = json.load(open('zappa_settings.json'))[
        'production']['environment_variables']['DATABASE_URL']
    JWT_SECRET_KEY = 'your-secret-key'
    # Needed to validate tokens
    GOOGLE_CLIENT_ID = '1092564513780-fffffffffffffffffffff.apps.googleusercontent.com'

    @staticmethod
    def init_app(app):
        pass


class DevelopmentConfig(Config):
    # Should still set --debug flag when running flask run
    DEBUG = True
    AWS_PROFILE_NAME = 'diced'


class ProductionConfig(Config):
    AWS_PROFILE_NAME = 'default'


config = {
    'development': DevelopmentConfig,
    'default': DevelopmentConfig,
    'production': ProductionConfig,
}

```



```python
from flask import request, current_app, make_response

#Use current_app to access config
@bp.route("/google_login", methods=["POST"])
def google_login():
    if not request.is_json:
        return make_response("Missing JSON in request", 400)
    token = request.json.get('token', None)
    try:
        idinfo = id_token.verify_oauth2_token(
            token, requests.Request(), current_app.config['GOOGLE_CLIENT_ID'])

```

