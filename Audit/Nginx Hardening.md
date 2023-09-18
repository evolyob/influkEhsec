
```php
>> not installed (disabled)
//不建議使用模組
nginx -V 2>&1 | egrep '|||'
- http_dav_module
- http_gzip_module
- http_gzip_static_module
- autoindex module
  #egrep -i '^\s*autoindex\s+' /etc/nginx/nginx.conf
  #egrep -i '^\s*autoindex\s+' /etc/nginx/conf.d/*

>> User nginx is not allowed to run sudo
//不允許使用者sudo執行
  #passwd -S "$(awk '$1~/^\s*user\s*$/ {print $2}' /etc/nginx/nginx.conf | sed -r 's/;.*//g')"
  #chown -R root:root /etc/nginx
***Default Value: 660  --->755

>> directories and files is restricted
// 目錄及檔案應受限制
  #chown root:root /var/run/nginx.pid
***Default Value: 644
```
path : /etc/nginx/nginx.conf
```php
>> audit all listening ports on the server
// 檢查nginx使用port
  #grep -ir "listen[^;]*;" /etc/nginx
***Default Value: Only port 80

>> Ensure timeout is 10 seconds or less, but not 0
//確認逾時設定應 1秒 -> 10秒
  #grep -ir keepalive_timeout /etc/nginx
  #keepalive_timeout 10;
***Default Value: none
  #grep -ir send_timeout /etc/nginx
  #send_timeout 10;
***Default Value: send_timeout 60s;

>> Server_tokens directive is set to `off`
   #server {
      ...
     server_tokens off;
      ...
}
***Default Value: on

>>Default error and index.html pages do not reference NGINX
Edit
   - /usr/share/nginx/html/index.html 
   - usr/share/nginx/html/50x.html
remove -->> any lines that reference NGINX.

>>Hidden file serving is disabled
  #grep location /etc/nginx/nginx.conf
Remediation:
  #location ~ /\. { deny all; return 404; }
***Default Value: none
```
```php
>>Reverse proxy does not enable information disclosure
Remediation:  ngx_http_proxy_muodule
#location /docs {
.... 
proxy_hide_header X-Powered-By;
proxy_hide_header Server;
....
}
***Default Value: none
```
```php
>> Access/error logging is enabled
   #grep -ir access_log /etc/nginx
   #access_log off;
Remediation:
access_log /var/log/nginx/host.access.log main;
error_log /var/log/nginx/error_log.log info;
***Default Value: none

>>Ensure proxies pass source IP information
Remediation: ngx_http_proxy_muodule
server {
    ...
location / {
        proxy_pass (Insert Application URL here);
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
         }
}
```
```php
>> HTTP is redirected to HTTPS
Remediation:
server {
  listen 80;
  server_name <hostname>;
  return 301 https://$host$request_uri;
}
***Default Value:none

>> Only modern TLS protocols are used
Web Server:
server {
 ssl_protocols TLSv1.2 TLSv1.3;
 ssl_ciphers EECDH:EDH:!NULL:!SSLv2:!RC4:!aNULL:!3DES:!IDEA;
 }
Proxy:
location / {
  proxy_pass <hosturl>;
  proxy_ssl_protocols TLSv1.2 TLSv1.3;
  proxy_ssl_ciphers EECDH:EDH:!NULL:!SSLv2:!RC4:!aNULL:!3DES:!IDEA;
  }
***Default Value: HIGH:!aNULL:!MD5.

>> HTTP Strict Transport Security (HSTS)is enabled
Remediation:
server {
  add_header Strict-Transport-Security "max-age=15768000;" always;
  add_header Strict-Transport-Security "Strict-Transport-Security: max-age=31536000; includeSubDomains; preload";
}
***Default Value: none

>> HTTP/2.0 is used
Remediation:
server {
  listen 443 ssl http2;
}
***Default Value: HTTP/1.1



Remediation:
client_body_timeout 10; client_header_timeout 10;
***Default Value:
client_header_timeout 60; client_body_timeout 60;

>>Maximum request body size
Remediation:
client_max_body_size 100K;
***Default Value:
client_max_body_size 1m;

>>Maximum buffer size for URIs
Remediation:
large_client_header_buffers 2 1k;
***Default Value:
large_client_header_buffers 4 8k;

>>Connections per IP address is limited
Remediation:
http {
  limit_conn_zone $binary_remote_addr zone=limitperip:10m;
  server {
        limit_conn limitperip 10;
        }
}
***Default Value:
none

```
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
     client_body_timeout 10;           //Default : 60
     client_header_timeout 10;         //Default : 60  
     large_client_header_buffers 2 1k;     //Default :4 8k;
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
      


location / {
        try_files $uri $uri/ /index.php?$query_string;

        client_max_body_size 10m;
        proxy_pass (Insert Application URL here);
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	
    }
```
