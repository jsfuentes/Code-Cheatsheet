# Setup

### Installation

Have python installed  

```bash
python --version

poetry run python --version
```



```
pip install Django
python -m django --version

poetry add Django
poetry run python -m django --version
```

### Setup Project

```bash
poetry run django-admin startproject musicbot
cd musicbot
poetry run python manage.py startapp polls
```

### Setup DB

In `settings.py` under DATABASES

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'musicbot',
        'USER': 'musicbot_user',
        'PASSWORD': 'SOMETHINGSOMETHING',
        'HOST': 'dpg-ce111111111111ep5d0-a.oregon-postgres.render.com',
        'PORT': '5432',
    }
}
```

postgres://musicbot_user:ezEYFLbxQc6kgL48rkoYQHgVKhCydJiL@dpg-ce1c4g2rrk09esbep5d0-a.oregon-postgres.render.com/musicbot

```
python manage.py migrate
```

### Plug in App

`settings.py`

```python
INSTALLED_APPS = [
    'polls.apps.PollsConfig', #add app name
    'django.contrib.admin',
    'django.contrib.auth',
    ...
]
```

## React

```
poetry add django-cors-headers
```

`settings.py`

```python
INSTALLED_APPS = [
    'django.contrib.admin',
		...
    'corsheaders',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
		...
    'corsheaders.middleware.CorsMiddleware',
]

#.......rest of file

CORS_ORIGIN_WHITELIST = [
     'http://localhost:3000'
]
```

Create api routes probably using a serializer
