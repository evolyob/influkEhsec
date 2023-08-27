#### kali cli
```php
nano = vim  
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
nc -nv //netcat
Nmap= TCP Scan= http ftp telnet
UDP= dns dhcp snmp
nmap -vv -sU -Pn -T4 --top-ports 200 <traget>
nmap -Pn --top ports 1000 -sU --stats-every 3m --max-retries 1 -T3 <traget>
nmap -vv -p <port> --script=all <target>// find the vunl
--version-intensity<0-9> //查詢資料庫的深度範圍是 0 ~ 9，預設是 7
-sV //(Connect)列舉開啟服務的詳細版本
-Pn //跳過刺探步驟，直接進行掃描
-sT -O //(Connect)去猜測檢測目標的作業系統版本
-oN <logfile> //輸出到 logfile 檔案與螢幕上
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
dnsrecom -d <target> -t axfr
ftp snmp smtp
```
```php
kioptrix level 1
netcat
connecting listening
bind shells
reverse shells
nc -nv <target> // port scan
nc -nvlp <target>// listening




```
