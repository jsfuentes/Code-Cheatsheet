## EC2(Elastic Compute)

### Creation

[Great 5 min Coursera Video Launching Instance](https://www.coursera.org/learn/aws-fundamentals-going-cloud-native/lecture/Bk9bp/creating-a-web-server-using-amazon-ec2)

[Go here and launch instance](https://us-east-2.console.aws.amazon.com/ec2/v2/home?region=us-east-2#Instances:sort=dnsName)

- 1 AMI(Amazon Machine Instance): machine configuration like hardware and software
- 3 Instance Details: VPC and subnets, roles(ocmmunication between services), user data under advanced(define scripts to run on startup)
- 5 Tags: add some details 
- 6: Security Group: who can access instance, 80 port, 0.0.0.0 means anyone can access rather then specific IP's 
- Final: Choose key pair to access instance(Virgil.pem for you Jorge)

Get your key

### SSH

ssh with your key into EC2 

Key must be 400 permission `chmod 400 [keypath].pem`

[More info here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)

`ssh -i [key file] [default AMI username]@[public DNS address or IPv6]`

e.g `ssh -i "~/Desktop/virgil.pem" ec2-user@ec2-13-59-254-214.us-east-2.compute.amazonaws.com`

### Usage

For default Linux image: `sudo yum install git`
git clone your repo

Install dependencies with yum find name with` sudo yum list | grep python` seems anything after dash is dep idk

Make sure your server is running on port 80 and go wild

Use public ip address to access in browser: 18.223.158.210

##### Python3

`sudo yum install python3`

