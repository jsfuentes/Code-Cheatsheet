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

Easy enough to do, select the bucket

Make sure to set **Default Root Object** to the index.html or whatever

## Using your own domain

Must have certificate validating you own the domain, ACM offers something, but must be us-east-1

