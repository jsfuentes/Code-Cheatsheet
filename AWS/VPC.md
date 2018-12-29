# Virtual Private Cloud (VPC)

You control all resources inside VPC, can create subnets that isolate parts 

10.10.0.0/16 : means first 16 bits are frozen 

Makes this the total VPC



10.10.1.0/24 means first 24 bits are frozen

## IGW

All connections with subnet through internet gateway 

Attach it, add route table

## Create a private subnet

Good for databases that shouldn't be accessed by outside

Inside VPC can access each other 

### Multiple Zones Elastic Load Blancer

Launch many private subnets on another zone for high avalibility 

Use elastic load blancer to do it between subnets



