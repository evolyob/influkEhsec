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

10. Detect Botnet connections IPS
資安管理設定 -> 入侵偵測防禦 --> botnet ---> Botnet C&C (block)

11. Ensure Antivirus Definition Push Updates are Configured
Under "FortiGuard Updates" ensure that the "Scheduled updates" is set to "Automatic".
系統管理 -> FortiGuard --> FortiGuard更新 ---> 排成更新 ----> 全自動

12.
config antivirus settings
set machine-learning-detection enable

set outbreak-prevention block
Use FortiGuard outbreak prevention database" is enabled.
資安管理設定 -> 防毒配置 -->  病毒突發防護--->使用突發性防護資料庫---->啟用

13.Enable Botnet C&C Domain Blocking DNS Filter
Security Profiles > DNS Filte   Redirect botnet C&C requests to Block Portal" is enabled.
資安管理設定-> DNS過濾 --> 重導botnet C&C 訪問要求到阻擋頁面--->  啟用
資安管理設定-> DNS過濾 -->選項 --->記錄所有DNS詢問及回應--->  啟用
```

```php
14.Block high risk categories on Application Control
Validate that "P2P" and "Proxy" category is blocked.
資安管理設定-> 應用程式控制 --> 點進後 分類 ---> proxy, p2p ---->blocked
資安管理設定-> 應用程式控制 --> 點進後 分類 ---> 未知應用程式  ----> 監控

15.Block applications running on non-default ports
Security Profiles > Application Contro >Block applications detected on non-default ports >enable
資安管理設定-> 應用程式控制 --> 點進後 分類 ---> 選項 在非標準埠號阻擋此應用程式---->啟用
Apply Application Control Security Profile to Policies
??資安管理設定-> 應用程式控制 --> 點進後 分類 ---> 網路協定強制符規設定---->啟用
```
```
16.Enable Compromised Host Quarantine 受損主機隔離
Security Fabric > Automation > Compromised Host Quarantine
安全織網-> 自動化動作 --> 動作
?????????
```
VPN
```
17.Apply a Trusted Signed Certificate for VPN Portal
System > Certificates > Import
系統管理-> 憑證 -->  檢查信任的憑證

18.maximum login attempts and lockout period
set auth-lockout-threshold 5
set auth-lockout-duration 300
用戶&認證-> 身分驗證設置 -->  使用者認證選項 ---> 認證逾時 5分鐘

```
```
19.Enable Event Logging
Log & Report > Log Settings  >  Enable "All" Event Logging
日誌與報表-> 紀錄設置 -->  紀錄設定 --->  事件紀錄 ----> 全部
```
