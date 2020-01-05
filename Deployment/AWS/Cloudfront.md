# Cloudfront

CDN allowing faster responses with global distribution for static content

Also can be used for EC2 with some sort of API speed up

Pretty easy to setup with good tool tips

### Pricing

AWS Free Tier includes 50GB data transfer out, 2,000,000 HTTP and HTTPS Requests with Amazon CloudFront.

you don’t pay for any data transferred between these services and CloudFront

### Uses

- Create a CDN for Amazon S3, Amazon EC2 or Elastic Load Balancing
- Add Https to S3 static site

Features

- Restrict content to certain geographic regions

## Add To S3 Static Site

AWS WHY?

- DONT SELECT THE SUGGESTED BUCKET
- DO NOT SET *Default Root Object* PROPERTY!
- Instead use the actual url of the S3 static site

## Using your own domain

Must have certificate validating you own the domain, ACM offers something, but must be us-east-1

