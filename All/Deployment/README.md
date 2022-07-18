# Deployment Solutions

Infrastructure as a service:

- AWS
- GCP
- Azure

Platform as a service:

- Heroku (Best Always Free Tier with both DB and Compute)
- AWS EBS
- Render (Startup out of Stripe that is excellent combo of cheap/easy, no free tier rn)

Static Site Servers:

- [Vercel](https://vercel.com)

- [Netlify](https://www.netlify.com/)
- Surge

AWS(iass) vs Heroku Platform as a service(pass)

Costs for Heroku can be about 3x, but as easy as a git push and many additional apps, as easy as increasing number of dynos

## Questions to Ask

- Timed Jobs Seperate?
- Analytics
  - Google Analytics?
  - Logging?
  - Usage Stats
- Database
  - Service
  - Capacity
  - Backups
- Server Running
  - Frontend Serving ?
  - Nginx, load balancing?
  - Backend
  - Autoscaling? Hanlding load spikes
  - Auto restart
- HTTPs certificate?
- Continuous Deployment?, Github hooks?

