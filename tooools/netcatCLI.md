#Netcat
```php
connecting listening
bind shells
reverse shells
>> PortScan
nc -nv <target> // port scan
nc -nvlp <target>// listening

-n  // ip address no DNS
-v  // verbose use -vv get more
-p  // 指定port
-l  // 開始監聽
-u  // use UDP mode
-w  // 超時設定
-t  // telnet應答?
-z  // 直接顯示結果

>  //文件輸出
nc -lp 5555 > balo.jpg  //把監聽5555輸出到在balo.jpg裡面

<  //文件輸入
nc -nv <target><port> < balo.jpg  //balo.jpg傳輸到 <target><port> 
```
