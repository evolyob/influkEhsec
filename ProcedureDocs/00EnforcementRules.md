#### （一）	網路安全
```php
 1	為防止不當使用網路，應依網路使用狀況與條件、主機與使用者工作內容等原則，區隔不同網路區段。
 2	連線正式作業環境應使用必要防護措施及雙因子身分驗證機制。
 3	因業務之故需要進行遠距工作者，需事先提出申請，並透過安全加密連線機制（如:VPN），由外部網路連線至內部網路，並進行適當的存取權限控管
 4	每年應至少一次檢視防火牆規則應評估其必要性。
 5	外部存取服務如非有迫切的作業需求，應儘量避免常態性開放，僅於必要時經確認後作暫時性開放，使用結束後即予以關閉。
 6	保有各網路設備、主機或資通系統之電腦稽核紀錄（Log）的有效性與關聯比較需求，應設定時間同步服務指向同一時間來源。
 7	隨時注意監控網路的運作，如非法來源IP短時間持續性刺探或被重復阻擋對網路及主機連線行為，應即時啟動緊急應變處理程序。
```
#### （二）	資訊設備
```php
1	預設識別碼及密碼，除無法修改者外，應於安裝後立即更改。
2	應關閉非必要之預設功能並限制其他設備使用者可存取之服務。
3	應每半年至少一次進行主機弱點掃描，弱點掃描報告之高風險等級弱點，應優先處理；中風險、低風險等級之弱點，得考量處理能量，做適當處理並紀錄
4	辦理設備維護保養、設備韌體更新、日誌(Log)、設定檔(Config)等，應確認記錄保存完整性。
```

#### （三）	識別碼及密碼
```php
1	應定期檢視已逾期之臨時或緊急帳號事後追蹤補申請單。
2	資訊系統帳號不得交付他人使用，應避免多人共用同一個帳號為原則。
3	作業系統中只允許必要之帳號存在，非必要之帳號應予刪除
4	一般使用者密碼長度須設定至少8碼；特權管理帳號12碼、密碼複雜度如：P@sSw0rD(英文大小寫、數字及特殊符號等字元)。
5	若密碼是驗證唯一驗證途徑需至少每90天變更1次，且密碼不得與帳號相同；超過使用效期後45天未變更應停用或做妥善處理。
6	硬體設備、應用軟體、系統軟體之最高權限帳號或具程式異動、參數變更權限之帳號應列冊及保管機制；最高權限帳號使用時須先取得權責主管同意，並保留稽核軌跡。
```

#### （四）	資料備份與還原
```php
1	主要系統服務之所有必要資料應每週進行完整備份，應保存至少五年。
2	次要網路設備、應用系統及資料庫相關設定檔應每季進行備份。
3	應保存全部重要系統與相連之防護設備之日誌紀錄（Log）（作業系統日誌、網站日誌、應用程式日誌、登入日誌），並定期備份於異機至少留存6個月以上紀錄。
4	日誌紀錄應包含登入帳號、系統功能、時間、系統名稱、IP來源、查詢指令等。
```

#### （五）	安全開發政策
```php
1	應儘量避免修改套裝軟體，如需修改應加以控管。
2	為減少可能影響作業系統運作之風險，應用程式之更新作業應限定由授權之管理人員執行。
3	應將安全需求要項納入系統功能，此安全需求應包含系統容量、資源、權限管理等。
4	停止弱點修補或更新之系統軟體與應用軟體，如有必要應採用必要防護措施。
5	開發環境、測試環境與正式作業環境應區隔成不同的設備及網段，限制所能存取的應用程式及資料庫，以保護正式作業環境系統及資料。
6	應避免提供涉及個人隱私之真實資料作測試，應先進行資料遮蔽處理或管制保護。
7	變更應事先通知並保留足夠的時間，供系統負責人進行審查和測試，應由二人以上進行並留存相關紀錄。
8	應建立開發套件特定版本、環境相依性、Libery Source、recommended function、must not function、單元測試、crytpgraphy relate and Hash Function及特定使用情境需求等。
```
