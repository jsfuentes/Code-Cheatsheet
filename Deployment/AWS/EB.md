## Elastic Beanstalk(EB)

Elastic Beanstalk is a fancy wrapper for EC2 instance with like load-balancing and shit

Doesn't cost more to use this service then the underlying resources:

- security group
- load balancer
- auto scaling configuration & group
- Ec2 - good to configure logs streaming
- S3
- Cloudwatch

## Deployment Types

All at once - <1 min for one EC2 and just takes down servers and sends update

Rolling – one batch at a time stopping and reverting on failure. Reduced capacity

Rolling with additional batch – Start and deploys on a batch, then rolling so no reduced capacity. But extra time to spin up new instance

Immutable – Deploy to new single instance, starts by deploying your application code to a single  newly created EC2 instance. Once the deployment succeeds on the first  instance, the remaining number of instances required to create a  parallel fleet are created and the application code is deployed to them. After the deployment succeeds on the entire parallel fleet, instances  running the old application version are terminated 25% at a time. This  deployment policy ensures that the impact of a failed deployment is  minimal (i.e.: a single EC2 instance) and enables your application to  serve traffic at full capacity during an ongoing deployment.





## Initialize on the Command Line

In the coding directory, run these commands for nice step by step creation

```bash
brew installing eb cli 
eb init
eb create
```

### Usage

```bash
eb open # to see
eb deploy # to deploy last commit
```

## Initialize In Console

Defaults are pretty minor without a load balancer and just a micro

Software - Nodejs default startup is app.js, index.js, then npm start; can set start command thought. 

Security - Can set key to ssh into EC2 here

## Internal Usage

`/var/app` is where app is deployed

Check the logs in cloudwatch or in the logs tab

##### Bugs

##### Website error after eb open

 Make sure to run website on the right port(usually 80 for the web)

