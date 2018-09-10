# AWS

## EC2 Instance
Create one online at Amazon
Get your key
ssh with your key into EC2
yum install git
git clone your repo
Make sure your server is running on port 80 and go wild

## Shitty Elastic Beanstalk
Elastic Beanstalk is a fancy wrapper for EC2 instance with like load-balancing and shit

## Installing

brew installing eb cli was ez
make amazon account


#### EB Command Line
In the directory these are the relevant Commands, they got a nice step by step creation

`eb init`
`eb create`

To see
`eb open`

To repush
`eb deploy`

## Bugs
Website error after eb open
  Port 80 for the web

## Codebuild

Input: Github Link or zipped file in S3

Output: Build artifacts or upload Docker image to ECR

Very versatile with the phases running arbitrary bash scripts

To build Docker images, you need to allow privileged access or use the AWS Ubuntu Docker runtime which lets u use the Docker daemon for building