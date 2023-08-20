### AccessControl 存取控制
依各業務系統範圍內具硬體設備、應用軟體、系統軟體之最高權限帳號或具程式異動、參數變更權限之帳號應定期盤點並考量權限最小化及存在必要性，詳如下述階段性實施說明:

1. Level 1
```yaml
 - PasswdLength   密碼長度須設定至少 12碼，勿使用預設或命名像預設之帳號執行維運。
 - PasswdComplex  密碼複雜度設定宜具英文大小寫、數字及特殊符號等字元(P@sSw0rD)。
 - PasswdChange   若密碼是驗證唯一驗證途徑需90天變更一次。
//參考指令 : cat /etc/pam.d/system-auth
```
2. Level 2
```yaml
 - UserAccount    使用者帳號應僅具唯讀及查詢功能權限。
 - PrivilegeGroup 特權管理帳號應定期清查並保留稽核日誌。
 - AP Account     程式執行帳號應定期確認業務相依性並保留稽核日誌。
//參考指令 : cat /etc/group
```
3. Level 3
```yaml
 - AuditLog       作業系統日誌、網站日誌、應用程式日誌、登入日誌應定期備份於異機至少留存 6個月以上紀錄。    
 - AccessPath     依業務需求應限制存取路徑。
 - SSH Key        程式執行帳號應使用金鑰驗證執行存取，並有專人管理。
```
4. Level 4
```yaml
   MFA            維運人員應利用兩種以上認證因素後獲得存取權限進入正式區伺服器。
   (Multi-Factor Authentication) 
   -OTP (oneTimePassword) 一次性密碼
   -SSO (singleSignOn)    短時間內單一認證登入
   -Token                 指定獨立裝置進行驗證
```
