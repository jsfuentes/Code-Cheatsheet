# Django

MVC web framework from 2003

- comes with ORM, form system, template, caching, middleware support, unit testing, and internationalization

## Running

```bash
poetry run python manage.py runserver
poetry run python manage.py runserver 4000 #set port
poetry run python manage.py shell #shell with settings.py so DB access
```

## Basics

#### Default Project Files

- mysite/
      [manage.py](https://docs.djangoproject.com/en/4.1/ref/django-admin/) - same as django-admin but uses settings.py
      mysite/
          \__init__.py
          [settings.py](https://docs.djangoproject.com/en/4.1/topics/settings/)
          [urls.py](https://docs.djangoproject.com/en/4.1/topics/http/urls/) - routes
          asgi.py - entrypoint for asgi web servers
          wsgi.py - entrypoint for wsgi web servers

### Default App Files

- polls/
      \__init__.py
      admin.py
      apps.py
      migrations/
      	\__init__.py
      models.py
      tests.py
      urls.py
      views.py
