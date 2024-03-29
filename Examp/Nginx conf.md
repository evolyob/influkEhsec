```php
    .....
server {
    listen 443 ssl http2;
    server_name  <URI>;

    root  /path;
    index index.php index.html;

     charset utf8;
     access_log  /var/log/nginx/....-access.log main;
     error_log  /var/log/nginx/....-error.log;
     keepalive_timeout 65s;            //Default: none
     send_timeout 10s;                 //Default: 60
     client_body_timeout 10s;           //Default: 60
     client_header_timeout 10s;         //Default: 60  
     large_client_header_buffers 2 1k;     //Default:4 8k;
     server_tokens off;                //Default: none
		
     ssl_certificate_key /etc/nginx/ssl/.....key;
     ssl_certificate /etc/nginx/ssl/....pem;
     ssl_session_cache shared:SSL:9m;
     ssl_session_cache shared:ssl_session_cache:10m;
     ssl_session_timeout 5m;
     ssl_stapling on;             //Default: none
     ssl_stapling_verify on;      //Default: none

     ssl_protocols TLSv1.2 TLSv1.3;
     ssl_ciphers 'EECDH+CHACHA20:EECDH+AES128:EECDH+AES256:!SHA1:!SHA256';
     ssl_prefer_server_ciphers on;

     add_header Set-Cookie "Path=/; HttpOnly; Secure";
     add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
     add_header X-Content-Type-Options nosniff;
     add_header X-Frame-Options "DENY";
     add_header Content-Security-Policy 
    }
location / {
        try_files $uri $uri/ /index.php?$query_string;

        client_max_body_size 10m;
        
        proxy_pass https://<uri:port>;    	        
	proxy_set_header Host $proxy_host;
        proxy_set_header X-Real-IP $remote_addr;  //自訂一個header變數，名稱可隨意設定
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  
	proxy_set_header X-Forwarded-Proto https;

        proxy_cache cache1;
        proxy_cache_lock on;
        proxy_cache_use_stale updating;
        proxy_force_ranges on;
        add_header X-Cache $upstream_cache_status;
    }
```


```php
設定 /etc/nginx/nginx.conf

vim /etc/nginx/nginx.conf


#worker_processes  auto;
worker_processes  8;
worker_rlimit_nofile 65535;

events {
    worker_connections  10240;
    use epoll;
}



http {
    fastcgi_intercept_errors on;


    access_log  /var/log/nginx/access.log  main;
    client_max_body_size 20m;


    sendfile        on;
    tcp_nopush      on;
    tcp_nodelay     on;
    server_tokens     off;

    keepalive_timeout  65;
```

```php
 移除 /etc/nginx/conf.d/php-fpm.con
cd /etc/nginx/conf.d

mv php-fpm.conf  php-fpm.conf.bak


NGINX 權限設定： php/session 資料夾改擁有者跟群組
###如果網頁發生 500 error 的問題，通常就是session目錄權限，原本是apache要改為nginx

cd /var/lib/php/
chown nginx:nginx /var/lib/php/session/
ls -ald /var/lib/php/session/

```
