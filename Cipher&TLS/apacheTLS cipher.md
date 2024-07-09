##### ref. CIS_Apache_HTTP_Server_2.4_Benchmark_V2.1.0

```
# 更新來源庫
apt update
# 檢查狀態
service apache2 status
# 查看版本
apache2 -v
# 啟用的模組
apache2ctl -M
```
```
# 強制移除風險模組
a2dismod --force autoindex status info.load userdir
a2dismod --force auth_digest auth_basic
```
```
apt install libapache2-mod-security2
cd /etc/apache2/mods-enabled
a2enmod headers

cd /etc/modsecurity
cp /etc/modsecurity/modsecurity.conf-recommended  /etc/modsecurity/modsecurity.conf

SecRuleEngine On
```
```
# 確認安全模組是否安裝
a2enmod ssl rewrite apparmor
/etc/init.d/apparmor start
# 再檢查啟用模組
apache2ctl -M
# 移除預設頁面
### rm /var/www/html/index.html
```
![image](https://hackmd.io/_uploads/Hyfna85vA.png)

```
https://owasp.org/www-project-modsecurity-core-rule-set/
```

```
/etc/apache2/mods-available/ssl.conf

SSLUseStapling on
SSLStaplingCache "shmcb:logs/stapling-cache(150000)"

# Disable waek ciphers
SSLCipherSuite AES256+EECDH:AES256+EDH:AES128+EECDH:AES128+EDH:!SHA1
SSLHonorCipherOrder On
SSLProtocol All -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
SSLSessionTickets Off
```
![image](https://hackmd.io/_uploads/Hy_VMwqP0.png)

```
vi /etc/ssl/openssl.cnf
CipherString = DEFAULT@SECLEVEL=2

#这将禁用弱密码套件，包括 SHA-1
openssl ciphers -v
```
![image](https://hackmd.io/_uploads/rJ04SNcwC.png)

```
/etc/apache2/apache2.conf
Timeout 10
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 15

LimitRequestline 512
LimitRequestFields 100
LimitRequestFieldsize 1024
LimitRequestBody 102400
RewriteEngine On

SSLInsecureRenegotiation off
SSLCompression off
```
![image](https://hackmd.io/_uploads/H1DLT85DA.png)
```
/etc/apache2/mods-available/reqtimeout.conf
RequestReadTimeout header=20-40,MinRate=500 body=20,MinRate=500
```

```
/etc/apache2/conf-available/security.conf
# 不顯示版本
ServerTokens Prod
ServerSignature off
# 禁止被Trace
TraceEnable Off
# headers 設定
Header always set X-Content-Type-Options nosniff
Header always set X-Frame-Options DENY
Header always set Strict-Transport-Security "max-age=63072000;
Header always set X-XSS-Protection "1; mode=block"
```



systemctl restart apache2
```
https://devsecopsguides.com/docs/checklists
https://webdock.io/en/docs/how-guides/security-guides/
