#### kali cli
```php
nano = vim  
mkdir  //new one 
rmdir  //delete one
locate  = find = which
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
nmap -vv -p <port> --script=all <target>
// find the vunl
-oN <logfile> //輸出到 logfile 檔案與螢幕上
MSF console // other portscan app
```

```php
ssh -c <cipherType> <target>
owasp dirbuster 


```
