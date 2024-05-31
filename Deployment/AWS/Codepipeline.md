# Code Pipeline

Has Input Layer (github, S3)

Has Build Layer (CodeBuild)

Has Deploy Layer (EBS, CodeDeploy)

Each Layer is defined in terms of inputs and outputs which are overriden from the defaults

## Notifications

In Cloudwatch Events, can listen for changes to code pipeline status and send notifications