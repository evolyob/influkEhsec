

```
path:  /etc/apache2/sites-enabled/default-ssl.conf
```
```
SSLProtocol -all +TLSv1.3 +TLSv1.2
SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH:!SHA
SSLOpenSSLConfCmd Curves X25519:secp521r1:secp384r1:prime256v1

SSLHonorCipherOrder on

Header always set X-Frame-Options SAMEORIGIN
Header always set Strict-Transport-Security "max-age=63072000;
Header always set X-Content-Type-Options nosniff
Header always set X-XSS-Protection "1; mode=block"
# (path: /etc/apache2/sites-available/)

Header always set Referrer-Policy "no-referrer, strict-origin-when-cross-origin"

SSLCompression      off
SSLUseStapling on
SSLSessionTickets   off

```

```
path /etc/httpd/conf/httpd.conf

SSLProtocol -All TLSv1.3 +TLSv1.2
SSLCipherSuite "EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH:!SHA1:"


#systemctl restart httpd
```
```



systemctl restart apache2
```
https://devsecopsguides.com/docs/checklists
https://webdock.io/en/docs/how-guides/security-guides/
