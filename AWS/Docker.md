# Docker in AWS

## EC2

Instance should be Linux 2 or AMI

```bash
sudo yum update -y

# Linux 2
sudo amazon-linux-extras install docker
#OR Linux
sudo yum install docker

sudo service docker start
sudo usermod -a -G docker ec2-user
```

Make sure to expose port 80 and then you can access it through the IP address