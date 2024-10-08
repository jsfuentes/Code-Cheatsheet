# AWS

Ondemand, online, pay as you go IT services

[Products](https://aws.amazon.com/products/)

[Explained Products](https://expeditedsecurity.com/aws-in-plain-english/)

Different regions offer different costs, latency, and compliance

## AWS CLI

Any command is using your default configuration IAM

`aws configure`

### Setup

[AWS CLI Setup](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-set-up.html)

Linux

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

Mac

```
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
```

[IAM Admin User Setup](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html)

### Security

AWS will give you info you need for compliance for its services, the things you control you need to control security

Encryption offered, security policies, with enough encryption we can't touch you

### Cost

Trused Advisor Dashboard, Cost Explorer, Pricing Calculator, AWS Budgets

Create reports, budgets for thresholds, notifications 

