| Merchant| Customer |
| :--:| :--: |
- - -
| //| WWW |API |CMS | # | Secure  |  Database | 
| :--:| :--: | :--: |:--:| :--: | :--: | :--: | 
| //|Bill |GW|OOO|#|Redis ||| 
| //| >>> | >>>|>>> |# | >>>|>>>|>>> |
| //|Image|Mail| DNS| #| Log|Tools| 
|//|NTP| Daemon |Update| #| |Monitor|
- - - 
| Bank| OA site |
| :--:| :--: |
#### Shutdown Priority
- [X] Web >> -- > API
#### Can't be Shutdown && Chk Priority
- [ ] Bill、GW、DB、
```php
1. 確認synclog還原壓縮檔
2. 複製母板 
3. snapshot 空機
4. tar解壓縮 web最新備份檔
5. ip、policy、mount...設定確認
6. 測試網頁是否正常顯示
7. 確認是否有log紀錄
8. 測試完成
```
