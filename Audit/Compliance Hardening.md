### chk cipher設定 22 port
/etc/crypo-polices/
```php
// vi /etc/crypto-policies/back-ends/openssh.config 
// vi /etc/crypto-policies/back-ends/opensshserver.config
// sshd -t
```
### chk FW开放port list
````
#firewall-cmd --zone=public --list-ports
````
### passwd policy list
```
/etc/pam.d/system-auth
```
### chk  XXX
```
/etc/pam.d/sshd
/etc/httpd/conf/httpd.conf
```
### root list
```
/etc/group
```
### chk
```
/etc/ssh/sshd_config
```

### chk Repository
```php
/etc/yum.conf
/etc/yum.repos.d/*.repo
##baseurl=https://****** 
##gpgcheck=1/0 
##gpgkey=***
##enabled=1
##module_hotfixes=true
```
### chk NTP設定
```
timedatectl  
chronyc tracking
```
### chk port list
```
netstat -ltupn
```
### 有啟用的服務
```
systemctl list-unit-files | grep service | grep enabled
```
### chk 現有排程
```
/etc/crontab
##***** root,command
/var/spool/cron
##crontab -e -u name
```
### log排程紀錄
```
vim /var/log/cron
```
### chk設定IP
```
vi /etc/sysconfig/network-scripts/ifcfg-ens192
##nmcli connection reload            #重新加載配置文件
##nmcli connection up ens192         #不重啟系統，讓網卡生效
##nmcli                              #查看IP詳情
````
### chk目前在哪層目錄下
```
pwd
```
### chk Nginx安在什麼地方
```
whereis nginx
```
## chk 環境設定
```php
/etc/sysctl.conf
#TCP读buffer
net.ipv4.tcp_rmem = 4096 131072 1048576

#TCP写buffer
net.ipv4.tcp_wmem = 4096 131072 1048576
```
```php
#为TCP socket预留用于发送缓冲的内存默认值（单位：字节）
net.core.wmem_default = 8388608

#为TCP socket预留用于发送缓冲的内存最大值（单位：字节）
net.core.wmem_max = 16777216

#为TCP socket预留用于接收缓冲的内存默认值（单位：字节）

net.core.rmem_default = 8388608

#为TCP socket预留用于接收缓冲的内存最大值（单位：字节）

net.core.rmem_max = 16777216

#每个网络接口接收数据包的速率比内核处理这些包的速率快时，允许送到队列的数据包的最大数目

net.core.netdev_max_backlog = 262144

#web应用中listen函数的backlog默认会给我们内核参数的net.core.somaxconn限制到128，而nginx定义的NGX_LISTEN_BACKLOG默认为511，所以有必要调整这个值

net.core.somaxconn = 262144
```
```php
#系统中最多有多少个TCP套接字不被关联到任何一个用户文件句柄上。这个限制仅仅是为了防止简单的DoS攻击，不能过分依靠它或者人为地减小这个值，更应该增加这个值(如果增加了内存之后)

net.ipv4.tcp_max_orphans = 3276800

#记录的那些尚未收到客户端确认信息的连接请求的最大值。对于有128M内存的系统而言，缺省值是1024，小内存的系统则是128

net.ipv4.tcp_max_syn_backlog = 262144

#时间戳可以避免序列号的卷绕。一个1Gbps的链路肯定会遇到以前用过的序列号。时间戳能够让内核接受这种"异常"的数据包。这里需要将其关掉

net.ipv4.tcp_timestamps = 0

#为了打开对端的连接，内核需要发送一个SYN并附带一个回应前面一个SYN的ACK。也就是所谓三次握手中的第二次握手。这个设置决定了内核放弃连接之前发送SYN+ACK包的数量

net.ipv4.tcp_synack_retries = 1

#在内核放弃建立连接之前发送SYN包的数量

net.ipv4.tcp_syn_retries = 1

#开启TCP连接中time_wait sockets的快速回收

net.ipv4.tcp_tw_recycle = 1

#开启TCP连接复用功能，允许将time_wait sockets重新用于新的TCP连接（主要针对time_wait连接）

net.ipv4.tcp_tw_reuse = 1
```
