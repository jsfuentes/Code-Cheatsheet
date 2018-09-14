# AWS

## EC2 Instance
Create one online at Amazon
Get your key
ssh with your key into EC2
`yum install git`
git clone your repo
Make sure your server is running on port 80 and go wild

## Shitty Elastic Beanstalk
Elastic Beanstalk is a fancy wrapper for EC2 instance with like load-balancing and shit

#### EB Command Line

brew installing eb cli was ez
make amazon account

In the directory these are the relevant Commands, they got a nice step by step creation

`eb init`
`eb create`

To see
`eb open`

To repush
`eb deploy`

##### Bugs

##### Website error after eb open
  Port 80 for the web

## Codebuild

Input: Github Link or zipped file in S3

Output: Build artifacts or upload Docker image to ECR

- Very versatile and simple basically running bash commands with some sugar for uploading and downloading and sdks api for kicking off in different languages

#### Uses:

- Kick off some scripts(async?) from APIs
- Build some code from github/s3 and output it to an S3

#### Notes

- To build Docker images, you need to allow privileged access or use the AWS Ubuntu Docker runtime which lets u use the Docker daemon for building

- Automagically unzips the file if your source is a zip

- Artifacts are searched for based on the base dir

#### Buildspec

```
version: 0.2

phases:
  pre_build:
    commands:
      - echo Building image
      - ls 
      - cd GraderFiles
  build:
    commands:
      - pwd
      - echo START PUBLIC LOG
      - docker build -t test .
      - echo END PUBLIC LOG
  post_build:
    commands:
      - docker image ls
      - docker save test -o test.tar
      - echo $CODEBUILD_SRC_DIR
artifacts:
  files:
    - test.tar

```

## S3

Basically nice filesystem as a service

S3 vs DB: S3 has no restrictions on what data can be added and can be huge files, DB restrictions and organization allows complex/faster queries

Uses:

- store files, images, videos, etc 
- could be used as a ghetto key value store or ghetto GitHub

### CLI

`aws s3 sync . s3://mybucket`

## AWS Lambda (Serverless)

run code without provisioning or managing servers

Uses:

- Runs code based on events like S3/DB changes
  - ETLs(Extract Transform Load for data analytics)
- Can be used as an API with Amazon API Gateway