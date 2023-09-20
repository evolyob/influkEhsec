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
     keepalive_timeout 20s;            //Default: none
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
        proxy_pass (Insert Application URL here);
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       
	proxy_cache_key             "$scheme$host$request_uri";
        proxy_cache                 STATIC;
        proxy_cache_valid           200  7d;
        proxy_cache_bypass  $http_cache_control;
        proxy_cache_use_stale       error timeout invalid_header updating
                                    http_500 http_502 http_503 http_504;
    }
```
