# Secrets

```bash
poetry add django-environ
```

In `settings.py`

```python
import environ

# Initialise environment variables
env = environ.Env()
environ.Env.read_env()
```

Then make a `.env`

```bash
SECRET_KEY=h^z13$qr_s_wd65@gnj7a=xs7t05$w7q8!x_8zsld
DATABASE_NAME=postgresdatabase
DATABASE_USER=alice
DATABASE_PASS=supersecretpassword
```

And finally, replace secretes with `env("SECRET_NAME")`

```python
DATABASES = {
	‘default’: {
		‘ENGINE’: ‘django.db.backends.postgresql_psycopg2’,
		‘NAME’: env(‘DATABASE_NAME’),
		‘USER’: env(‘DATABASE_USER’),
		‘PASSWORD’: env(‘DATABASE_PASS’),
	}
}
```