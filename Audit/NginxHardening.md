
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
```
