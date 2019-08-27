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

#### [Buildspec](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)

```
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