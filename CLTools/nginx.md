# Nginx

**NGINX** is open source software for web serving, reverse proxying, caching, load balancing, media streaming, and more.

Serves as an ultra fast middle man between a client and server

See AWS EC2 for installation

```bash
sudo vi /etc/nginx/nginx.conf
sudo /etc/init.d/nginx start

sudo nginx -s reload
```

## Configuration File

nginx and its modules configuration defined by `nginx.conf` and placed in the directory `/usr/local/nginx/conf`,`/etc/nginx`, or `/usr/local/etc/nginx`.

**Directives** are divided into simple directives and block directives.

If a block directive can have other directives inside braces, it is called a **context** (examples: [events](https://nginx.org/en/docs/ngx_core_module.html#events), [http](https://nginx.org/en/docs/http/ngx_http_core_module.html#http), [server](https://nginx.org/en/docs/http/ngx_http_core_module.html#server), and [location](https://nginx.org/en/docs/http/ngx_http_core_module.html#location)).

May include several server blocks for different ports/server names

Nginx decides which server processes a request by testing uri specified in request's header, selects one with longest prefix and passes rest of uri to route

### Serving Static Files

```nginx
worker_processes auto;

events { }

http {
    server {
    		#localhost/index.html => /data/www/index.html
        location / {
           root /data/www; 
        }
        #localhost/images/hi.png => /data/images/hi.png
        location /images/ {
           root /data;
        }
    }
}
```

### Reverse Proxy Server

```nginx
worker_processes auto;

events { }

server {
    listen 8080; #default port is 80
    root /data/up1; #will be used when not specified in location

    location / {
    }
}

server {
  	#proxy_passes to above server
    location / {
        proxy_pass http://localhost:8080;
    }
}
```

### Advanced

#### Regex URI

Preceded by ~ 

Precedent over normal prefix matches

```nginx
location ~ \.(gif|jpg|png)$ {
    root /data/images;
}
```



