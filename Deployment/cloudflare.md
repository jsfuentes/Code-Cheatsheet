# Cloudflare

Becomes your DNS provider and adds a cache layer in front of your server

Allows you to CNAME a root domain 

FREE SSL & FREE CACHING WTF

Very helpful support articles and UI

1) Add DNS Records

2) Go to ssl/tls and edge certificates to enable 

### Redirect non-www to www

Need record for both non-www and www

Add pagerule that redirect `example.com*` to `https://www.example.com/$1`

