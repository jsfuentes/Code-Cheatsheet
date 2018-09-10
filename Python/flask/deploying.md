# Deploying Options

## Simplest

`ngrok http [THE PORT YOU WANT]`

## Gunicorn

WSGI(python web server) recommended version

`gunicorn [OPTIONS] APP_MODULE` 

APP_MODULE means \$(MODULE_NAME):\$(VARIABLE_NAME)

## Heroku

Make `Procfile` in main folder to tell heroku what to do

Add line 

