# Heroku

1) `heroku create` : just create the url on the spot and add remote to repo

2) `git push heroku master`: push to heroku and build 

heroku open

`heroku local 

##### Tail logs

`heroku logs --tail`

### Node

`npm run start`

The command in a web process type must bind to the port number [specified in the `PORT` environment variable](https://devcenter.heroku.com/articles/dynos#local-environment-variables). If it does not, the dyno will not start.