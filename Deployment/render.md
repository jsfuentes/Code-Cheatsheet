# Render

Cheaper Paas than Heroku and nice UI, early stage startup that is active in the Elixir community

https://render.com/chat

## Elixir

[Deploy Phoenix With Releases](https://render.com/docs/deploy-phoenix)

[Change Elixir Version](https://render.com/docs/elixir-erlang-versions)

## Custom Domains

https://render.com/docs/custom-domains#configuring-dns-to-point-to-render

#### Yaml

Private services are the same as public web services, but they **don’t have a publicly accessible HTTPS URL**.

```yaml
services:
# A Docker web service
- type: web
  name: webdis
  env: docker
  repo: https://github.com/render-examples/webdis.git # optional
  region: oregon                                      # optional (defaults to oregon)
  plan: standard                                      # optional
  branch: master                                      # optional (uses repo default)
  dockerCommand: ./webdis.sh                          # optional (defaults to Dockerfile command)
  healthCheckPath: /
  envVars:
  - key: REDIS_HOST
    fromService:
      name: redis
      type: pserv
      property: host          # available properties are listed below
  - key: REDIS_PORT
    fromService:
      name: redis
      type: pserv
      property: port
  - fromGroup: conc-settings
# A private Redis instance
- type: pserv
  name: redis
  env: docker
  repo: https://github.com/render-examples/redis.git # optional
  envVars:
  - key: GENERATED_SECRET
    generateValue: true       # will generate a base64-encoded 256-bit secret
  - key: DASHBOARD_SECRET
    sync: false               # placeholder for a value to be added in the dashboard
  disk:
    name: redis-data
    mountPath: /var/lib/redis
    sizeGB: 10                # optional
# A Ruby web service
- type: web
  name: sinatra
  env: ruby
  repo: https://github.com/renderinc/sinatra-example.git
  numInstances: 3
  buildCommand: bundle install
  startCommand: bundle exec ruby main.rb
  domains:
  - test0.render.com
  - test1.render.com
  envVars:
  - key: STRIPE_API_KEY
    value: Z2V0IG91dHRhIGhlcmUhCg
  - key: DB_URL
    fromDatabase:
      name: elephant
      property: connectionString
  - key: REDIS_SECRET
    fromService:
      type: pserv
      name: redis
      envVarKey: GENERATED_SECRET
  autoDeploy: false             # optional
# A Python cron job that runs every hour
- type: cron
  name: date
  env: python
  schedule: "0 * * * *"
  buildCommand: "true"        # ensure it's a string
  startCommand: date
  repo: https://github.com/render-examples/docker.git # optional
# A background worker that consumes a queue
- type: worker
  name: queue
  env: docker
  dockerfilePath: ./sub/Dockerfile # optional
  dockerContext: ./sub/src    # optional
  branch: queue               # optional
# A static site
- type: web
  name: my blog
  env: static
  buildCommand: yarn build
  staticPublishPath: ./build
  pullRequestPreviewsEnabled: true     # optional
  headers:
  - path: /*
    name: X-Frame-Options
    value: sameorigin
  routes:
  - type: redirect
    source: /old
    destination: /new
  - type: rewrite
    source: /a/*
    destination: /a

databases:
- name: elephant
  databaseName: mydb          # optional (Render may add a suffix)
  user: adrian                # optional
  ipAllowList:                # optional (defaults to allow all)
  - source: 203.0.113.4/30
    description: office
  - source: 198.51.100.1
    description: home

- name: private database
  databaseName: private
  ipAllowList: []            # only allow internal connections

envVarGroups:
- name: conc-settings
  envVars:
  - key: CONCURRENCY
    value: 2
  - key: SECRET
    generateValue: true
  - key: USER_PROVIDED_SECRET
    sync: false
- name: stripe
  envVars:
  - key: STRIPE_API_URL
    value: https://api.stripe.com/v2
```

