```php
設定php-fpm.d/www.conf
vim /etc/php-fpm.d/www.conf

user = nginx
group = nginx

#42
;listen = /run/php-fpm/www.sock
listen = 127.0.0.1:9000

#105
;pm = dynamic
pm = static

;pm.max_children = 50
pm.max_children = 900

;pm.start_servers = 5
pm.start_servers = 500

;pm.min_spare_servers = 5
pm.min_spare_servers = 500

;pm.max_spare_servers = 35
pm.max_spare_servers = 900

;pm.max_requests = 500
pm.max_requests = 500


我新增設定
#333
request_slowlog_timeout = 2s       ;request_slowlog_timeout = 0
#348
rlimit_files = 65536               ;rlimit_files = 1024
```

```php
設定 /etc/php-fpm.conf
vim /etc/php-fpm.conf

#44
log_level = notice
#105
rlimit_files = 65536          ;rlimit_files = 1024

 設定 /etc/php.ini

#111
error_reporting=E_ALL&~E_NOTICE


#352
;realpath_cache_size = 4096k
realpath_cache_size = 4096k

;realpath_cache_ttl = 120
realpath_cache_ttl = 120

#400
#expose_php = On
expose_php = Off

#410
;max_execution_time = 30
max_execution_time = 600

;max_input_time = 60
max_input_time = 600

;memory_limit = 128M
memory_limit = 2048M

#594
error_log = "/var/log/php_error_log"

#700
;post_max_size = 8M
post_max_size = 200M

#852
;upload_max_filesize = 2M
upload_max_filesize = 10M

#879
;default_socket_timeout = 60
default_socket_timeout = 600      
        
#938
[Date]
; Defines the default timezone used by the date functions
; https://php.net/date.timezone
;date.timezone =
date.timezone = "Asia/Taipei"

#1365
;session.cache_expire = 180
session.cache_expire = 300
```
