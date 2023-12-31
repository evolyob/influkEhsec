#### nginx -v 1.24.0
/etc/nginx/conf.d
```yaml
ssl_protocols TLSv1.2 TLSv1.3;
ssl_ciphers 'EECDH+CHACHA20:EECDH+AES128:EECDH+AES256:!SHA1:!SHA256';

  add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
  add_header X-Content-Type-Options nosniff;
  add_header X-Frame-Options "DENY";
```
```yaml
systemctl restart nginx
nmap --script ssl-cert,ssl-enum-ciphers -p 443 172.16.xxx.xxx
```
#### Header chk
```yaml
curl -v -k https://<target> 2>&1 | egrep "Security|Options|Cookie"
```

#### XSS der header PRotect
```
- Strict-Transport-Security 
//only allow HTTPs connections
- Content-Security-Policy 
//enable XSS protection using CSP
- X-XSS-Protection 
//don't load pages with possible XSS attacks
- X-Frame-Options 
//don't allow to include our app into 3rd party apps via iframes
- X-Content-Type-Options 
//enable strict usage of MIME types
- Referrer-Policy 
//don't pass Referrer header to other websites that are being visited from our app
- Permissions-Policy 
//control which browsers APIs can be used by our app
```
```yaml
##Set-Cookie: Path=/; HttpOnly; Secure
##Strict-Transport-Security: max-age=31536000; includeSubDomains
##X-Content-Type-Options: nosniff
##X-Frame-Options: DENY
```
