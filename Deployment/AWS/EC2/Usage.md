##   EC2(Elastic Compute)

### Creation

[Great 5 min Coursera Video Launching Instance](https://www.coursera.org/learn/aws-fundamentals-going-cloud-native/lecture/Bk9bp/creating-a-web-server-using-amazon-ec2)

[Go here and launch instance](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#Instances:sort=dnsName)

- 1 AMI(Amazon Machine Instance): machine configuration like hardware and software
- 3 Instance Details: VPC and subnets, roles(ocmmunication between services), user data under advanced(define scripts to run on startup)
- 5 Tags: add some details 
- **6: Security Group**: who can access instance
  - To allow http traffic, need to allow TCP on port 80 with 0.0.0.0/0 represents anyone on ipv4 and ::/0 represents anyone on ipv6
  - To allow ssh traffic, port range 22
- Final: Choose key pair to access instance(main.pem for you Jorge)

Get your key

### SSH

ssh with your key into EC2 

Key must be 400 permission `chmod 400 [keypath].pem`

[More info here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)

```bash
ssh -i [key file] [default AMI username]@[public DNS address or IPv6]
```

e.g

```bash
ssh -i "~/Desktop/main.pem" ubuntu@ec2-18-222-213-113.us-east-2.compute.amazonaws.com
```

Default AMI username for Ubuntu is `ubuntu` and for linux ami is `ec2-user`

