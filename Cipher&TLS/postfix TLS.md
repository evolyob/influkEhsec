- [x] <https://www.postfix.org/TLS_README.html>
- [x] <https://access.redhat.com/articles/1468593>

```bash
vi /etc/postfix/main.cf

smtpd_tls_security_level = may


smtpd_use_tls = yes
smtpd_tls_mandatory_protocols = !SSLv2, !SSLv3, !TLSv1, !TLSv1.1
smtpd_tls_protocols = !SSLv2, !SSLv3, !TLSv1, !TLSv1.1
smtpd_tls_exclude_ciphers = EXP, MEDIUM, LOW, DES, 3DES, SSLv2, aNULL, SHA, DH
disable_vrfy_command=yes

```
當所有請求集中在一起轉發到 back-end server 時
如果在這之中有不合法的請求的話，此不合法的請求會被當成下一個請求被 back-end server

CVE-2023-51764 postfix: SMTP smuggling vulnerability

```
vi /etc/postfix/main.cf

smtpd_forbid_unauth_pipelining = yes
```
```
postfix reload
```
