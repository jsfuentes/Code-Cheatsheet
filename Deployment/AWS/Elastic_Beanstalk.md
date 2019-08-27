## Shitty Elastic Beanstalk

Elastic Beanstalk is a fancy wrapper for EC2 instance with like load-balancing and shit

Doesn't cost more to use this service then the underlying resources:

- security group
- load balancer
- auto scaling configuration & group
- Ec2 - good to configure logs streaming
- S3
- Cloudwatch

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
eb deploy # to repush
```

## Internal Usage

`/var/app` is where app is deployed

Nodejs will run `npm run start` on build 

##### Bugs

##### Website error after eb open

 Make sure to run website on the right port(usually 80 for the web)

