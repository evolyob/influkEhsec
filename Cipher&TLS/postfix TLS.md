https://www.postfix.org/TLS_README.html
https://access.redhat.com/articles/1468593

```bash
vi /etc/postfix/main.cf

smtpd_tls_security_level = may


smtpd_use_tls = yes
smtpd_tls_mandatory_protocols = !SSLv2, !SSLv3, !TLSv1, !TLSv1.1
smtpd_tls_protocols = !SSLv2, !SSLv3, !TLSv1, !TLSv1.1
smtpd_tls_exclude_ciphers = EXP, MEDIUM, LOW, DES, 3DES, SSLv2, aNULL, SHA, DH
disable_vrfy_command=yes

```

