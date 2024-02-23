---
title: Ghost Docker
feed: hide
date : 23-02-2024
---


For Ghost, I use port `8001`. If you prefer another, please change it to your preferred port.

```
version: '3.1'

  

services:

	ghost:
		image: ghost:latest
		restart: always
		ports:
			- "8001:2368"
		environment:
			database__client: mysql
			database__connection__host: db
			database__connection__user: ghost
			database__connection__password: pass
			database__connection__database: ghost
		url: http://<your-domain>.com
		depends_on:
			- db
	db:
		image: mysql:5.7
		restart: always
		environment:
			MYSQL_ROOT_PASSWORD: pass
			MYSQL_DATABASE: ghost
			MYSQL_USER: ghost
			MYSQL_PASSWORD: pass
		volumes:
			- ghost-db:/var/lib/mysql
volumes:
	ghost-db:
```



```
server {
    listen 80;
    server_name <your-domain>.com www.<your-domain>.com;

    location / {
        proxy_pass http://127.0.0.1:8001;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```