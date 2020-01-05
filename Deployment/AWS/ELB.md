# ELB (Elastic Load Balancing)

Regional highly available to route traffic to different EC2 or IP address

## 3 Types

**Application Load Balancer** operates at the request level (layer 7), routing based on request contents. Ideal for HTTP/HTTPS load balancing

**Network Load Balancer** operates at the connection level (Layer 4), routing within Amazon Virtual Private Cloud (Amazon VPC) based on IP protocol data. Ideal for load balancing of both TCP and UDP traffic. Lower level so faster and able to handle sudden and volatile traffic 

**Classic** is for EC2 Classic

## Adding HTTPS

You can add a listener for HTTPS at port 443, must have SSL Certificate in same region

To make http redirect to HTTPS, need to add a ngnix configuration script to .ebextensions, check out [this for an example](https://github.com/jsfuentes/Node-Base/tree/master/.ebextensions)