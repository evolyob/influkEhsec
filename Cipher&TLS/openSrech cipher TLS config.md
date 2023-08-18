- [x] <https://opensearch.org/docs/latest/security/configuration/tls/>

#### vi /etc/opensearch/opensearch.yml
```yaml
plugins.security.ssl.transport.enforce_hostname_verification: false
###
plugins.security.ssl.transport.enabled_protocols:
 - "TLSv1.3"
 - "TLSv1.2"
plugins.security.ssl.transport.enabled_ciphers:
 - "TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384"
 - "TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256"
 - "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
 - "TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384"
 - "TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256"
 - "TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA"
 - "TLS_CHACHA20_POLY1305_SHA256"
 - "TLS_AES_256_GCM_SHA384"
 - "TLS_AES_128_GCM_SHA256"
###
```
```yaml
plugins.security.ssl.http.pemtrustedcas_filepath: root-ca.pem
###
plugins.security.ssl.http.enabled_protocols:
 - "TLSv1.3"
 - "TLSv1.2"
plugins.security.ssl.http.enabled_ciphers:
 - "TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384"
 - "TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256"
 - "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"
 - "TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384"
 - "TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256"
 - "TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA"
 - "TLS_CHACHA20_POLY1305_SHA256"
 - "TLS_AES_128_GCM_SHA256"
 - "TLS_AES_256_GCM_SHA384"
###
```
```bash
systemctl restart opensearch
nmap --script ssl-enum-ciphers -p 9xx0 172.16.xxx.xxx
```
