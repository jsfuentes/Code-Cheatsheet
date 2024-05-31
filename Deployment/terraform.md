# Terraform

Infrastructure as code across cloud infrastructure

Use backend so it knows the existing resources so can update correctly (if theres real world drift you can import changes to terraform)

Use modules to define how to use bigger underlying resources

## Usage

Common to seperate files, main.tf, outputs.tf, variables.tf.

main.tf

```terraform
terraform {
	required_version = ">= 1.5"
	required_providers {
		aws = {
			source = "hashicorp/aws"
			version = ">=5.0"
		}
	}
	
	backend "s3" {
		 key = "prod/aws_ec2_keypair/terraform.tfstate"
	}
}

provider "aws" {
	region = var.aws_region
	profile = var.aws_profile
}

resource "aws_key_pair" "keypair" {
	key_name = "prod"
	public_key = "ssh-rsa JIPOJDFIOPSJMDVUIERUIOHEWFDSJNJLKNLDSDFERW"
}

#Fetch remote data
data "aws_vpc" "vpc" {
  id = "akakaf"
}

#Fetch remote data about other terraform files like vpc
data "terraform_remote_state" "vpc" {
  backend = "s3"
  config = {
    bucket = "optix-terraform"
    key="prod/aws_vpc/terraform.tfstate"
    region = var.aws_region
    profile = var.aws_profile
  }
}

locals {
  vpn_arc = data.aws_vpc.vpc.arn
}

#Reuse terraform code, like declarative function call
module "bastion_instance" {
  #source of code 
	source = "../../../modules/aws_opensearch_cluster"
  
  #pass variables to that module
  aws_account = ...
}
  
resource "hi" {
  
}
```

variables.tf

```terraform
variable "aws_region" {
  description = "AWS region"
}

variable "aws_profile" {
  description = "AWS profile"
}
```

- We set the env variables by certain script

output.tf

```terraform
output "name" {
  description = "EC2 keypair name"
  value       = aws_key_pair.keypair.key_name
}

output "public_key" {
  description = "EC2 keypair public key"
  value       = aws_key_pair.keypair.public_key
}

```

## File structure

- Environment
  - Prod
    - aws_ec2_bastion
  - Staging
    - aws_ec2_bastion
- Modules
  - aws_ec2_bastion
- Script

Environments have modules, terrafrom block, 

Modules don't have provider, must be used in higher order module

### Usage of Specific Setup

Go into file like `terraform/environments/prod/aws_elasticcache_redis_cluster`

#### New

```
source scripts/setup_terraform_local_env.sh
cd terraform/environments/prod/aws_elasticcache_redis_cluster
terraform init
terraform plan
```

#### Existing

```bash
terraform apply
```

//in chicken egg problems like vpc model might need to specific what goes first

```
terraform apply -target module.vpc
```

