
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
 ssl_ciphers ALL:!EXP:!NULL:!ADH:!LOW:!SSLv2:!SSLv3:!MD5:!RC4;
 }
Proxy:
location / {
  proxy_pass <hosturl>;
  proxy_ssl_protocols TLSv1.2 TLSv1.3;
  proxy_ssl_ciphers ALL:!EXP:!NULL:!ADH:!LOW:!SSLv2:!SSLv3:!MD5:!RC4;
  }

>> HTTP Strict Transport Security (HSTS)is enabled
Remediation:
server {
  add_header Strict-Transport-Security "max-age=15768000;" always;
  add_header Strict-Transport-Security "Strict-Transport-Security: max-age=31536000; includeSubDomains; preload";
}
***Default Value: none


```
