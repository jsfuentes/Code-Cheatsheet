# Process Management

Easily start and stop processes and look at

- pm2
  - pm2 monit
- http://supervisord.org/
-  [Let’s Encrypt](https://letsencrypt.org/) - running [certbot](https://certbot.eff.org/)

## Pm2

Application manager for node

Easily start and stop background node processes, 

| Cmd                | Effect                         |
| ------------------ | ------------------------------ |
| pm2 list           | list process                   |
| pm2 monit          | monitor connections in cool UI |
| pm2 start app.js   | Start                          |
| pm2 stop app.js    |                                |
| pm2 restart app.js |                                |

Might also do some cool logging