
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
>> directories and files is restricted
//
  #chown root:root /var/run/nginx.pid
>> audit all listening ports on the server
  #grep -ir "listen[^;]*;" /etc/nginx
>> Ensure keepalive_timeout is 10 seconds or less, but not 0
  #grep -ir keepalive_timeout /etc/nginx
  #keepalive_timeout 10;


```
