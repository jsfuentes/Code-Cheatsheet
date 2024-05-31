# Serverless

Framework to simplify deploying on aws lambda

## Usage

package.json with commands

``` 
{
  "scripts": {
    "deploy:staging": "sls deploy --stage staging",
    "deploy:prod": "sls deploy --stage prod",
    "local": "npm run build && sls invoke local --function getInference --path event-theme.json",
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {},
  "dependencies": {}
}
```

.serverless.yml

```
service: avatar-inference-service
provider:
  name: aws
  stage: ${opt:stage, 'staging'}
  region: us-west-2
  profile: aws-default
  timeout: 120
  environment:
    ENV: ${self:provider.stage}
  iam:
    role:
      statements:
        - Effect: Allow
          Action:
            - dynamodb:PutItem
            - dynamodb:Query
          Resource: arn:aws:dynamodb:us-west-2:024457260985:table/InferenceResponse-${self:custom.appsync_api_id.${self:provider.stage}}-${self:provider.stage}
        - Effect: Allow
          Action:
            - s3:PutObject
            - s3:PutObjectAcl
            - s3:DeleteObject
            - s3:GetObject
            - s3:ListBucket
          Resource: arn:aws:s3:::${self:custom.bucket_name.${self:provider.stage}}*
functions:
  getInference:
    handler: src/index.handler
    events:
      - sqs:
          arn:
            Fn::GetAtt:
              - AvatarInferenceQueue
              - Arn

resources:
  Resources:
    AvatarInferenceQueue:
      Type: AWS::SQS::Queue
      Properties:
        QueueName: avatar-inference-queue-${self:provider.stage}.fifo
        VisibilityTimeout: 3000
        FifoQueue: True

custom:
  appsync_api_id:
    staging: 3yze44ygpfhb7nvqtn3hoaa6hy
    prod: yzycbefp4zcizd3c6xquflibtu
  bucket_name:
    staging: optimatik-optix-staging
    prod: optimatik-optix-prod
```

