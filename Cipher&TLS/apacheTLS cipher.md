

```
path:  /etc/apache2/sites-enabled/default-ssl.conf
```
```
SSLProtocol -all +TLSv1.3 +TLSv1.2
SSLOpenSSLConfCmd Curves X25519:secp521r1:secp384r1:prime256v1

SSLHonorCipherOrder on

Header always set X-Frame-Options DENY
Header always set X-Content-Type-Options nosniff

SSLCompression      off
SSLUseStapling on
SSLSessionTickets   off

```
```



systemctl restart apache2
```
