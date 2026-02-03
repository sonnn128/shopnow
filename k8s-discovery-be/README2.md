-- template editor
```
- docker image
- port app
- app name
- namesspace
```

-- add hosts - forward to load balancer
```
192.168.1.101: là load-balancer
192.168.1.101 shopnow.nobison.online
192.168.1.101 api-shopnow.nobison.online
192.168.1.101 service-a.nobison.online
192.168.1.101 service-b.nobison.online
192.168.1.101 service-c.nobison.online
# vi /etc/nginx/conf.d/upstream.conf

```
```
upstream my_servers {
    server 192.168.1.105:30080
    server 192.168.1.106:30080
    server 192.168.1.107:30080
}
# vi /etc/nginx/conf.d/shopnow-frontend.conf
```
--

```
server {
    listen 80;
    server_name shopnow.devopsedu.vn;

    location / {
        proxy_pass http://my_servers;
        proxy_redirect off;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        try_files $uri $uri/ /index.html;
    }
}
```