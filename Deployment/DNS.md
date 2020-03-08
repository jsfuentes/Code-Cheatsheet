# DNS

## Basic Setup

![https://namecheap.simplekb.com//SiteContents/2-7C22D5236A4543EB827F3BD8936E153E/media/azurenew1.png](https://namecheap.simplekb.com//SiteContents/2-7C22D5236A4543EB827F3BD8936E153E/media/azurenew1.png)

****

On namecheap, set TTL to automatic and ez quick update. Can take days or very fast

## Record Types

https://www.namecheap.com/support/knowledgebase/article.aspx/434/2237/how-do-i-set-up-host-records-for-a-domain

| Record                                                       | Explanation                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| CNAME(Canonical Name)                                        | alias one name to another, must point to  domain name, must have unique name among records, never use for root domain name (e.g. example.com). |
| [A (Address)](https://www.namecheap.com/support/knowledgebase/article.aspx/319/2237/how-can-i-set-up-an-a-address-record-for-my-domain) | associate host with IPv4 address                             |
| [AAAA (IPv6)](https://www.namecheap.com/support/knowledgebase/article.aspx/319/2237/how-can-i-set-up-an-a-address-record-for-my-domain) | associate host with IPv4 address                             |
| ALIAS                                                        | record maps a name to another name, but can coexist with other records on that name. |
| URL Redirect Record                                          | Redirect to URL, masked means to keep the original url in the bar, unmasked means to change url |

Common to create: 

-  `A` record for `example.com` => server IP address

-  `CNAME`record for `www.example.com` => `example.com`

## Advanced

#### Multiple Servers, One Domain

Can also use **nginx** as a reverse proxy to use the url path as DNS only deals with domain name and subdomains

Use different hosts with CNAME records

I.e api.example.com => aws.backend1.com 

example's.com => aws.frontend.s3.com

### Example

| Type                | Host  | Value                          |
| ------------------- | ----- | ------------------------------ |
| CNAME Record        | jorge | d1onwfufhbfdtv.cloudfront.net. |
| CNAME Record        | www   | secure.pageserve.co.           |
| URL Redirect Record | @     | http://www.modulo.blog/        |

See AWS/cloudfront to see how to set that shit up

#### Http

Need certificate, note *.slingshow.com isnt the same as slingshow.com

### Testing

Perform a DNS query

```bash
host www.modulo.blog
```

Test https

https://decoder.link/sslchecker/modulo.blog/443