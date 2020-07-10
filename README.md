# Nginx SSL

## More Info

"Kevin J Jones - Securing Your Containerized Applications with NGINX"
https://www.youtube.com/watch?v=spVQex_qj_s&list=WL&index=2&t=1153s

## SSL Report

https://www.ssllabs.com/ssltest

## Generate stronger DH parameters

```
openssl dhparam -out /etc/ssl/certsdhparam.pem 4096
```

For highest security, It is recommended to use a bit length of 4096

## Proxy Pass

Use a proxy_pass directive to configure NGINX to resolve embedded Docker DNS server; this will support any scaling of your services while using Docker Compose

```
user nginx;

events {
	worker_connections 1024;
}
http {
	server {
		listen 80;
		location /login {
			proxy_pass http://login:80;
		}
	}
}
```

## Sidecar Proxy

Deploying NGINX as a Sidecar Proxy provides the ability to optimize TLS, standarize on HTTP protocol behavior and offload functionality that is already designed into NGINX without the need of developing it as code, such as authentication and authorization.

Using proxy_pass you can route requests to your application listening on localhost within the container

```
http {
	server {
		listen 80;
		server_name partner.example.com;
		location /api/v2 {
			proxy_pass http://127.0.0.1:5001;
		}
	}
}
```


