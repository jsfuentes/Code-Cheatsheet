# Deploying Options

## Simplest

`ngrok http [THE PORT YOU WANT]`

## EC2

To access over docker or AWS, must run flask development server **which should never be used** like this:

`    app.run(debug=True, host='0.0.0.0')`

**never do this**: `sudo pipenv run flask run -h 0.0.0.0 -p 80` 

## Gunicorn

WSGI(python web server) recommended version

`gunicorn [OPTIONS] APP_MODULE` 

APP_MODULE means \$(MODULE_NAME):\$(VARIABLE_NAME)

## Heroku

Make `Procfile` in main folder to tell heroku what to do

Add line 

