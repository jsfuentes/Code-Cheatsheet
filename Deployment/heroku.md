# Heroku

```bash
npm install -g heroku
```

### Deploy

Just creates url on the sport and adds remote(heroku) to repo(if run in git root)

Pushing to heroku builds and deploys

```bash
heroku create
git push heroku master 
heroku open
```

- Use `git push heroku cdn:master` to push a branch

#### Procfile

Add a textfile to root to configure, usually not required

### Usage

`heroku open`
`heroku local` 

##### Tail logs

`heroku logs --tail`

## Platforms

### Node

`npm run start`

The command in a web process type must bind to the port number [specified in the `PORT` environment variable](https://devcenter.heroku.com/articles/dynos#local-environment-variables). If it does not, the dyno will not start.

## Advanced

#### [Env Variables](https://devcenter.heroku.com/articles/config-vars)

```bash
 heroku config:set NODE_CONFIG_DIR=./server/config
```

### [Custom Domain](https://devcenter.heroku.com/articles/custom-domains)

1. `heroku domains:add nibble.blog` & ``heroku domains:add www.nibble.blog`, do for **BOTH**
2. The command will return a DNS target like `adjacent-beyond-4gewdoomo52mqsps2xp87wns.herokudns.com`
3. Set a CNAME record to the returned DNS Target for www(or both @ and www on cloudlfare) or ALIAS for @

### Different Price Tiers

| Dyno Type     | Memory (RAM) | CPU Share | Compute | Dedicated | Sleeps                                                       |
| :------------ | :----------- | :-------- | :------ | :-------- | :----------------------------------------------------------- |
| free          | 512 MB       | 1x        | 1x-4x   | no        | [yes](https://devcenter.heroku.com/articles/free-dyno-hours#dyno-sleeping) |
| hobby         | 512 MB       | 1x        | 1x-4x   | no        | no                                                           |
| standard-1x   | 512 MB       | 1x        | 1x-4x   | no        | no                                                           |
| standard-2x   | 1024 MB      | 2x        | 4x-8x   | no        | no                                                           |
| performance-m | 2.5 GB       | 100%      | 11x     | yes       | no                                                           |
| performance-l | 14 GB        | 100%      | 46x     | yes       | no                                                           |

**All**: [Specifying custom domains](https://devcenter.heroku.com/articles/custom-domains), [Pipelines](https://devcenter.heroku.com/articles/pipelines)

**Hobby-tier dynos+**:

- Free SSL and [automated certificate management](https://devcenter.heroku.com/articles/automated-certificate-management) for TLS certs
- [Application metrics](https://devcenter.heroku.com/articles/metrics)
- [Heroku Teams](https://devcenter.heroku.com/articles/heroku-teams)

**Standard-tier dynos+**:

- [Horizontal scalability](https://devcenter.heroku.com/articles/scaling)
- [Preboot](https://devcenter.heroku.com/articles/preboot)
- [Language runtime metrics](https://devcenter.heroku.com/articles/language-runtime-metrics)

**Performance-tier dynos**:

- [Autoscaling for web dynos](https://devcenter.heroku.com/articles/scaling#autoscaling)
- Dedicated compute resources

### Pushing a Directory

If you want to deploy a subdirectory: 

```bash
heroku create
heroku git:remote -a [APP_NAME] #from prev step
git subtree push --prefix [PATH_TO_SUBDIRECTORY] heroku master
heroku open
```

Force push: 

```bash
git subtree split --prefix server -b heroku-server
git push -f heroku heroku-server:master
```

