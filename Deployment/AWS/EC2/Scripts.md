# Scripts

## Ubuntu

##### All

```bash
sudo apt-get update
```

##### Nginx

```
sudo apt-get install nginx
sudo service nginx start

sudo vi /etc/nginx/nginx.conf
sudo /etc/init.d/nginx start

sudo nginx -s reload #reload on after change
```

##### Misc

```bash
sudo apt-get install tmux
sudo apt-get install python-pip
```

##### Docker

```bash
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ${USER} #restart so it takes effect
docker swarm init
```

##### Codedeploy Agent

```bash
sudo apt-get install ruby
sudo apt-get install wget
cd /home/ubuntu
wget https://[bucket-name].s3.[region-identifier].amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto

sudo service codedeploy-agent start
sudo service codedeploy-agent status #check
```

Wget link must be updated with proper [link for region](https://docs.aws.amazon.com/codedeploy/latest/userguide/resource-kit.html#resource-kit-bucket-names)

## Usage Default Linux Image

```bash
sudo yum update -y
sudo yum install -y git
```

Install dependencies with yum find name with` sudo yum list | grep python` seems anything after dash is dep idk

Make sure your server is running on port 80 and go wild with Docker or whatever

Use public ip address to access in browser: 18.223.158.210

##### Installing Other Common Deps

```bash
sudo yum install python3
sudo yum install nginx
```

##### Node

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash #nvm
. ~/.nvm/nvm.sh #activate
nvm install node
node -e "console.log('Running Node.js ' + process.version)" #test
```

##### Puppeteer

```bash
sudo amazon-linux-extras install epel -y
sudo yum install -y chromium
# npm i package.json with puppeteer, sftp scripts, then run 
```

##### Docker

```bash
sudo yum install -y docker
sudo service docker start
sudo usermod -a -G docker ec2-user #need to relog, to use docker without sudo
```

##### CodeDeploy Agent

```bash
sudo yum install -y httpd
sudo yum install -y git
sudo yum install -y ruby
sudo yum install -y wget
cd /home/ec2-user
wget https://bucket-name.s3.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
```

#### [Cloudwatch Logging Agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/download-cloudwatch-agent-commandline.html)

```bash
wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm
sudo rpm -U ./amazon-cloudwatch-agent.rpm
#IAM roles add CloudWatchAgentServerPolicy to EC2
```

Didnt seem to work….



