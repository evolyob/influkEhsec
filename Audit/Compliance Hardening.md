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
### chk  pam config
```
/etc/pam.d/sshd
```
### root list
```
/etc/group
```
### chk
```
/etc/ssh/sshd_config
ClientAliveInterval 900
ClientAliveCountMax 0

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
