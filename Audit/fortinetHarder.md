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


```
