## Codebuild

Input: Github Link or zipped file in S3

Output: Build artifacts or upload Docker image to ECR

- Very versatile and simple
- basically running bash commands with some sugar for uploading and downloading and sdks api for kicking off in different languages

#### Uses:

- Kick off some scripts(async?) from APIs
- Build some code from github/s3 and output it to an S3

#### Notes

- To build Docker images, you need to allow privileged access or use the AWS Ubuntu Docker runtime which lets u use the Docker daemon for building
- Automagically unzips the file if your source is a zip
- Artifacts are searched for based on the base dir

### [Buildspec](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)

buildspec.yml

```yaml
version: 0.2

phases:
	install:
		runtime-versions:
			java: openjdk8
      nodejs: 10
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

### Artifacts

- `'**/*'` represents all files recursively.
- `my-subdirectory/*` represents all files in a subdirectory named *my-subdirectory*.
- `my-subdirectory/**/*` represents all files recursively starting from a subdirectory named *my-subdirectory*.

## Example 2 Running AWSCLI

Need to allow access for the codebuild machine with IAM

- add policy S3FullAccess for S3

```yaml
version: 0.2

phases:
  install:
    runtime-versions:
      nodejs: 10
    commands:
      - npm i npm@latest -g
      - pip install --upgrade pip
      - pip install --upgrade awscli
  pre_build:
    commands:
      - echo Building iframe question
      - ls
      - cd plugin/src/iframe_question
      - npm install
  build:
    commands:
      - npm run build
  post_build:
    commands:
      - echo $CODEBUILD_SRC_DIR
      - pwd
      - aws s3 sync build s3://ecstatic-iframe-plugin
```

