####  Computer Configuration\Policies\Windows Settings\Security Settings\
#### 電腦設定\原則\Window設定\安全性設定\
```py
密碼原則
使用可還原加密來存放密碼   已停用
密碼必須符合雜湊需求性     已啟用
密碼最常使用期限    90 days
密碼最段使用期限     2 days
強行執行密碼歷程記錄 3 ages
最小密碼長度        12
```
```py
帳戶鎖定原則
允許系統管理帳戶鎖定   已啟用
重設帳戶鎖定計時器的時間間格   15mins
帳戶鎖定時間       15 mins
帳戶鎖定閥值       5 times
```
本機原則\使用者權限指派
```py
允許本機登入              adminstrators
//允許透過遠端桌面服務登入   adminstrators
//以批次工作登入            adminstrators

拒絕以批次工作登入           guests
拒絕以服務方式登入           guests
拒絕本機登入                guests
拒絕從網路存取這台電腦       guests
拒絕透過遠端桌面服務登入     guests

//偵錯程式                 adminstrators
//強制從遠端系統進行關閉    adminstrators
//從網路存取這台電腦        adminstrators

關閉系統                 adminstrators
//變更系統時間
//變更時區
```
本機原則\安全性選項
```py
MS網路用戶端
//傳送未加密的密碼   已停用
//數位簽章用戶端的   已啟用
數位簽章用戶端的   已啟用 ***

互動式登入
不要顯示上次登入              已啟用
//要求網域控制站驗證已解除鎖定   已啟動

帳戶
Guest帳戶狀態  已停用
重新命名系統管理員帳戶                 **** Guest  --->  guess
重新命名來賓帳戶名稱                   **** Admintrators ---> admintrat
//限制使用空白密碼的本機制帳戶僅能登入   已啟用

網域控制台
LDAP伺服器簽章要求           要求簽章
//允許伺服器操作者排程工作      已停用
//拒絕電腦帳戶密碼變更          已停用
LDAP伺服器通道連結權杖要求    一律

網路存取  
不允許SAM帳戶和共用的匿名        已啟用
//不允許SAM帳戶的匿名列舉          已啟用
不允許存放網路驗證的密碼語認證    已啟用
允許匿名SID/名稱轉譯             已停用
共用和安全性模式用於本機帳戶      傳統，本機 使用者以自身身分驗證
//限制匿名存取具名管道和共用        已啟用
//讓EVERYONE權限套用到匿名使用者   已停用

網路安全性
LAN Manager驗證等級              只傳送NTLMv2回應，拒絕LM & NTLM
NTLM SSP為主的(....)             要求NTLMv2工作階段安全性，要求128位元加密
NTLM SSP為主的(....)             要求NTLMv2工作階段安全性，要求128位元加密
設定Kerboeros允許加密類型         AES256_HMAC_SHA1, 未來的加密類型

關機
允許不登入就將系統關機             已停用
```
####  Computer Configuration\Policies\Windows Settings\Security Settings\
```py
系統服務
Print Spooler  已停用
```
#### 進階稽核原則設定\稽核原則
```py
帳戶登入
稽核認證驗證                  成功與失敗    usr失敗 ***
稽核Kerboeros驗證服務         成功與失敗    usr失敗 ***
稽核Kerboeros服務票證操作      成功與失敗

帳戶管理
稽核應用程式群組管理      成功與失敗   usr 失敗 ***
稽核電腦帳戶管理             成功     usr null
稽核發布群組管理             成功     usr 成功
稽核其他帳戶管理事件          成功    usr null
稽核安全性群組管理            成功    usr null
稽核使用者帳戶管理        成功與失敗   usr 失敗 ***

//詳細追蹤
//稽核PNP活動                 成功   usr null
//稽核建立處理程序             成功   usr null

DS存取
稽核目錄服務存取             失敗   usr 失敗 ***
稽核服務變更                 成功   usr 成功 ***

登入/登出
稽核帳戶鎖定               成功   usr null
稽核群組成員資格           成功   usr 成功
稽核登出                   成功   usr null
稽核登入              成功與失敗  usr 成功與失敗  ***
稽核特殊登入               成功   usr null

物件存取
稽核詳細的檔案共用            失敗   usr 失敗 ***
//稽核檔案共用            成功與失敗   usr 失敗 ***

原則變更
稽核驗證原則變更                成功   usr null
稽核授權原則變更                成功   usr 成功 ***
//稽核MPSSVC規則層級原則變更   成功與失敗 usr 成功與失敗 
稽核其他變更事件                失敗    usr 失敗 ***

系統
稽核其他系統事件          成功與失敗   usr null
稽核安全性狀態變更        成功與失敗   usr null
稽核安全性系統延伸        成功與失敗   usr 成功 ***
稽核系統完整性            成功與失敗   usr null
```
### Computer Configuration\Policies\Administrative Templates\
#### 系統管理範本\ Windows元件
```py
MS Defender 防毒軟體
MAPS\ 設定MS地圖報告的本機設定複寫  已停用   usr null

惡意探索防護\攻擊面減少             已啟用   usr null
/// 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2, , 26190899-1602-49e8-8b27-eb1d0a1ce869,3b576869-a4ec-4529-8536-b80a7769e899, 
/// 5beb7efe-fd9a-4556-801d-275e5ffc04cc, 75668c1f-73b5-4cf0-bb93-3ecf5cb7cc84, 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c, 92e97fa1-2edf-4476-bdd6-9dd0b4dddc7b, b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4, be9ba2d9-53ea-4cdc-84e5-9b1eeee46550, d3e037e1-3eb8-44c8-a917-57927947596d, and d4f940ab-401b-4efc-aadc-ad5f3c50688a,
/// are each set to a value of 1

即時保護
關閉即時保護                 已停用   usr null
開啟行為監視                 已啟用   usr null
掃描所有下載檔案及附件        已啟用   usr null
啟用指令碼掃描                已啟用   usr null
```

```py
Windows powershell
打開Poweshell指令區碼塊紀錄    已啟用   usr null
打開Poweshell轉譯             已停用   usr null


Windows遠端管理WinRM\WinRM用戶端
允許基本驗證                   已停用   usr 已停用 ***
允許未加密的流量               已停用   usr 已停用 ***
不允許WinRM儲存RunAs認證       已啟用   usr null

Windows遠端管理WinRM\WinRM服務
允許基本驗證                    已停用   usr 已停用 ***
允許未加密的流量                已停用   usr 已停用 ***
不允許WinRM儲存RunAs認證        已啟用   usr null

```
### Computer Configuration\Policies\Administrative Templates\
#### 系統管理範本\ Windows元件
```py
事件紀錄服務
安全性
指定紀錄檔大小上限(KB)                   已啟用
\\\  196,608 KB
控制記錄檔達到其大小上限時實踐記錄檔行為   已停用  usr 已停用 ***

安裝
指定紀錄檔大小上限(KB)                   已啟用
\\\  32,768 KB
控制記錄檔達到其大小上限時實踐記錄檔行為   已停用  usr 已停用 ***

系統
指定紀錄檔大小上限(KB)                   已啟用
\\\  196,608 KB
控制記錄檔達到其大小上限時實踐記錄檔行為   已停用  usr 已停用 ***

應用程式
指定紀錄檔大小上限(KB)                   已啟用
\\\  32,768 KB
控制記錄檔達到其大小上限時實踐記錄檔行為   已停用  usr 已停用 ***
```
```py
搜尋
允許加密檔案索引                          已停用  usr 已停用 ***

認證使用者介面
提升權限時列舉系統管理原帳戶               已停用  usr null

遠短桌面服務\遠短桌面工作階段主機\安全性
設定用戶端連線加密層級                    已啟用  usr 已啟用 ***
需要的RPC通訊                            已啟用  usr 已啟用 ***

遠短桌面服務\遠短桌面工作階段主機\暫存資料夾
結束後不刪除暫存資料夾                     已停用  usr 已停用 ***
不要使用每一工作階段的暫存資料夾            已停用  usr 已停用 ***

檔案總管
關閉殼層通訊協定受保護模式                 已停用  usr null
關閉檔案總管的資料執行防止                 已停用  usr null
損毀時關閉終止堆集                        已停用  usr null
```
### Computer Configuration\Policies\Administrative Templates\
#### 系統管理範本\ 系統
```py
區域系統管理員密碼解決方案(LAPS)
設定加密密碼歷程記錄大小                      已啟用 usr null
不允許密碼到期時間超過源則要求的時間           已啟用 usr null
密碼設定                                     已啟用 usr null

登入
防止使用者在登入時顯示帳戶詳細資料             已啟用  usr null
不要顯示網路選取UI                           已啟用  usr null

群組原則
設定登入原則處理                             已啟用  usr null
-- 在定期的背景處理期間不要套用
-- 即使群組源則物件尚未變更也進行處理

遠端協助
設定請求遠端協助                            已停用  usr 已停用 ***
設定提供管端協助                            已停用  usr 已停用 ***

稽核建立處理程序  
在建立處理程序是間中包含命令列                已啟用  usr 已啟用 ***
```
#### Computer Configuration\Policies\Administrative Templates\Control Panel\
### 系統管理範本\ 控制台
```py
個人化
防止啟用鎖定畫面像機                              已啟用  usr 已啟用 ***
防止啟用鎖定畫面頭影片放映                         已啟用  usr 已啟用 ***
```
#### Computer Configuration\Policies\Administrative Templates\
### 系統管理範本\網路
```py
DNS用戶端
關閉多點傳送名稱解析                               已啟用  usr 已啟用 ***

Lanman工作站    
啟用不安全的來賓登入                               已停用  usr 已停用 ***

Windows連線管理員
最小化忘記網路或Windows網域的平實連線數目            已啟用  usr 已啟用 ***
///  1  =  將同時連線最小化

網路連線
禁止在您的DNS網域網路上安裝、設定及使用網路橋接       已啟用  usr null
禁止在您的DNS網域網路使用網際網路連線共用            已啟用  usr 已啟用 ***
```

