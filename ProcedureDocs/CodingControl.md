
 CodingControl 開發維護控制
===
#### CodingControl
|  | Level 1 | Level 2| Level 3  |  Level 4 |
| --: | :--: |:--:| :--: | :--: |
| > | StrongCipher | AuthorityFlow | CrontabAlert| |
|>>  | SFTP Upload  |HotfixPolicy |VersionControl | 
| >>> | UnitTest | CI (SAST) | CD | CoreReview |
| >>>> | Knowhow  | Default  |  | Compatible |

>專案應考量設計、開發、測試、部署、維護階段之安全需求審查及風險管控機制。
>應建立開發套件特定版本、環境相依性、Libery Source、recommended function、must not function、單元測試、crytpgraphy relate and Hash Function及特定使用情境需求等。
>
>
>1. Level 1
>> - StrongCipher  強加密法版本(upto TLS1.2,SHA-2hash,AES crypto)底層設定
>> - SFTP Upload   不以明文傳輸資料或更新程式碼port 如:FTP、HTTP、SMTP
>> - UnitTest      單元檢查程式碼檢查後進 BetaTest
>> - Knowhow       常見漏洞程式邏輯認知(OWASPTop10)
```php
2. Level 2
 - AuthorityFlow 應考量單一功能單一授權流程 
 - HotfixPolicy  應定義緊急上板定義
 - CI            每次上板前應利用工具自動化檢查程式碼安全性
   (Continuous Integration)
```
### Level 3
 - CrontabAlert   應利用自動化排程設定檢查並具告警機制
 - VersionControl 每次上板應利用工具版本控制並保存紀錄
 - CD             上板應利用工具由二人以上檢核後自動佈版並留存相關紀錄。
  (Continuous Deployment)

####  Level 4
 - CoreReview      宜考量由第三方單位定期執行程式碼檢查
 - Compatible      宜定期考量服務使用套件更新版本之相容性
###

+ Scope:
+ for production’s data,option and config setting change requester.
+ Rules: 
+ requester and executor can’t be the same, it only be executed after obtaining the authorization by Reviewer.
+ but if it’s Immediate request that the Reviwer should be awared before executed,and submit all the documental recorded after executed.

### Hotfix definition:
1. Affect transactions.
2. The feature caused major customer complaints.
3. The overall performance will be affected.

