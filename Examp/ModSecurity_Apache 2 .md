```
mod_headers：隱藏安全資訊與設定內容安全政策
mod_security：網站應用程式防火牆阻擋攻擊 WAF
mod_evasive：防止 DDoS 攻擊
mod_ssl：建立安全加密的連線與確保資料完整性
mod_geoip：使用地理區域來允許或阻斷連線
```

```
apt install libapache2-mod-security2 -y

a2enmod headers
systemctl restart apache2
```

```
ModSecurity 設定檔
cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf
vi /etc/modsecurity/modsecurity.conf


# Enable ModSecurity, attaching it to every transaction. Use detection
# only to start with, because that minimises the chances of post-installation
# disruption.
#
SecRuleEngine On

```
設定 OWASP ModSecurity 核心規則集
```
刪除 ModSecurity 預設的規則集
rm -rf /usr/share/modsecurity-crs

OWASP-CRS 儲存庫複製到 /usr/share/modsecurity-crs 目錄中
git clone https://github.com/coreruleset/coreruleset /usr/share/modsecurity-crs

重命名 crs-setup.conf.example 為 crs-setup.conf
mv /usr/share/modsecurity-crs/crs-setup.conf.example /usr/share/modsecurity-crs/crs-setup.conf

重新命名預設請求排除規則檔案
mv /usr/share/modsecurity-crs/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf.example /usr/share/modsecurity-crs/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf
```

```
修改 Apache Security 設定檔
vi /etc/apache2/mods-available/security2.conf
```
```
<IfModule security2_module>
        # Default Debian dir for modsecurity's persistent data
        SecDataDir /var/cache/modsecurity

        # Include all the *.conf files in /etc/modsecurity.
        # Keeping your local configuration in that directory
        # will allow for an easy upgrade of THIS file and
        # make your life easier
        # IncludeOptional /etc/modsecurity/*.conf
        IncludeOptional /usr/share/modsecurity-crs/crs-setup.conf

        # Include OWASP ModSecurity CRS rules if installed
        # IncludeOptional /usr/share/modsecurity-crs/*.load
        IncludeOptional /usr/share/modsecurity-crs/rules/*.conf
</IfModule>
```

```
編輯虛擬主機設定檔
cd /etc/apache2/sites-available/
vi waf.your_domain.conf
```

```
設定 SecRuleEngine 為 On

<VirtualHost *:80>

    ServerName waf.your_domain

    Redirect permanent / https://waf.your_domain/

</VirtualHost>

<VirtualHost *:443>

    ServerName waf.your_domain

    ErrorLog ${APACHE_LOG_DIR}/error.log

    CustomLog ${APACHE_LOG_DIR}/access.log combined

    SecRuleEngine On

    ProxyPass / http://vmapplicationdev001.your_domain/

    ProxyPassReverse / http://vmapplicationdev001.your_domain/

    ProxyRequests Off

    SSLEngine On

    SSLCertificateFile /etc/apache2/ssl/server.crt

    SSLCertificateKeyFile /etc/apache2/ssl/server.key

</VirtualHost>

```

```
systemctl restart apache2
```

https://medium.com/@jieshiun/%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8-modsecurity-%E6%89%93%E9%80%A0-waf-%E7%B6%B2%E7%AB%99%E6%87%89%E7%94%A8%E9%98%B2%E7%81%AB%E7%89%86-4156bca1c8da
