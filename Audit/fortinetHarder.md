```php
1. disclaimer message  enable
  System' -> 'Replacement Messages' --> Extended View' --->Pre-login Disclaimer Message
  System' -> 'Replacement Messages' --> Extended View' --->Post-login Disclaimer Message
  系統管理 -> 替換訊息 -->延伸項目 --->登入前的免責聲明留言  啟用
  系統管理 -> 替換訊息 -->延伸項目 --->登入後的免責聲明留言  啟用

2.timezone is properly configured
  System -> 'Settings'--> Time Zone and NTP settings are under 'System Time'
  系統管理 -> 基本設定--> 系統時間 NTP
  Default Value:
  By default, Fortinet uses the NTPs server of the FortiGuard
  System -> 'Settings'--> hostname
  系統管理 -> 基本設定--> 主機名稱
```
```yaml
3. Disable USB Firmware and configuration
### config system auto-install
### get
config system auto-install
    set auto-install-config disable
    set auto-install-image disable
end
#### config system global
#### get
4. Disable static keys for TLS
config system global
    set ssl-static-key-ciphers disable
end
config system global
set admin-https-ssl-versions tlsv1-3

5. Enable Global Strong Encryption
config system global
    set strong-crypto enable
end
```
```php
6. Password Policy is enabled
  System -> 'Settings'--> Password Policy
  系統管理 -> 基本設定--> 密碼政策

config system password-policy
    set status enable
    set apply-to admin-password ipsec-preshared-key
    set minimum-length 8
    set min-lower-case-letter 1
    set min-upper-case-letter 1 set min-non-alphanumeric 1
    set min-number 1 set expire-status enable
    set expire-day 90
    set reuse-password disable
end
####    get system global
config system global
    set admin-lockout-threshold 3
    set admin-lockout-duration 60
    set admintimeout 10
    set admin-https-redirect disable //Default  enable
    set admin-port 8082              //Default 80 **(or any other uncommon port)** 
    set admin-server-cert "self-sign"
    set admin-sport 4343             //Default 443**(or any other uncommon port)**
end
```
### SNMP
```php
7. only SNMPv3 is enabled
  System -> SNMP
there is not any community for SNMPv1 or SNMPv2c and only SNMPv3 users are there. Also make sure that SNMP Agent is enabled
SNMPv1/v2c 空
SNMP v3
新增> 安全級別(認證)->認證演算法 sha512,變更密碼 -->Private加密演算法(AES256):密碼變更
### Remove 0.0.0.0 
```
```php
8. all the login accounts having specific trusted hosts

System -> Administrator ->edit ->allowed hosts / subnets are in the list of trusted Host
系統管理 ->  系統管理員  ->  編輯普通管理員 -> 限制管理由受信任主機登入 (啟用)  
### Remove 0.0.0.0

9. logging is enabled on all firewall policies
1.For allowed policies, "Log Allowed Traffic" is set on "All Sessions" option.
2.For denied policies, "Log Violation Traffic" is enabled.

10. Detect Botnet connections







```
