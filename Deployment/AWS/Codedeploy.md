# Codedeploy

Uses:

- run and build code on some group/ec2 instances
- Continuous Deployment with GitHub 

Target some group or ec2 instances and run and build code. then update the machines with rollback and load balancing managing it

Applications are groups of deployment groups which specify a target and IAM role to use when creating deployment

## Setup

Must have codedepoy agent installed and running on ec2 instance

For usage with autoscaling group, throw up an instance install codedeploy and right click instance and create AMI image

```bash
sudo service codedeploy-agent status
```

`/opt/codedeploy-agent/deployment-root/` holds the bundles downloaded and stores the last 5 deployments

## Appspec

Code deploy looks at the [appspec.yml](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file.html) file at your **root folder** to figure out what to dot

```
version: 0.0 #must be 0.0
os: linux #only linux and windows

files: #opt
  - source: /
    destination: /usr/estaticApp
    overwrite: true
    
permissions: #update permissions of files specified prev
  - object: /usr/estaticApp/codedeploy #only required
    pattern: "*.sh"
    owner: root
    group: root
    mode: 755
    type:
      - file #file or directory
      
hooks: #scripts to be executed
  BeforeInstall:
    - location: codedeploy/before_install.sh
      timeout: 1200
      runas: root
  AfterInstall:
    - location: codedeploy/after_install.sh
      timeout: 1201
  ApplicationStart:
    - location: codedeploy/app_start.sh
      timeout: 60
      runas: root
  ApplicationStop:
    - location: codedeploy/app_stop.sh
      timeout: 10
      runas: root

```

### LifeCycle Events

This is confusing and changes based on inplace deployments or blue/green

3600 max per app 

### Targets

EC2 Instances Tags, can run a deployment that runs a dep update or one time thing

Autoscaling, can attach to autoscaling gorup and codedeploy when new instance is needed

## Logs

Logs on ec2 can be viewed at 

`/opt/codedeploy-agent/deployment-root/deployment-logs/codedeploy-agent-deployments.log`

```
less /var/log/aws/codedeploy-agent/codedeploy-agent.log
```

### Bugs

If traffic lifecycles takes forever and there is a load balancer, the traffic depends on health checks defined by the target group

If nothing even starts, then you probably didnt install the codedeploy agent on the EC2s