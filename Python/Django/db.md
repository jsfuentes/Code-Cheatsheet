# Databases

Default is sqlite3 because it comes with python, but can use postgres and more

Default installed apps require a db and migrations

See setup.md for setup instructions

```bash
poetry run python manage.py sqlmigrate polls 0001 #to see what SQL will run
poetry run python manage.py check #check for db errors
```



