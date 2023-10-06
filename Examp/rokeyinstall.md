```php
5 選取相容性 --> 相容esxi7.0及更新版本
6 選取客體作業系統--> Rocky 選 其他 linux (64位元)
7 自訂硬體   ---> CPU:8  RAM:32 100GB 精簡佈建
    光碟機選 資料存放區ISO檔案
    -  time & date = asia/taipei timezone
    -  software Selection = minial intall
    - device type = LVM
    - file system = xfs
    - /home path disable
IPv4 Setting
DNS server --->>
adderss--netmask--gateway
```

```php
 uuidgen ens192                                  ///uuidgen產生新卡uuid
vi /etc/sysconfig/network-scripts/ifcfg-ens192    ///設定IP
nmcli connection reload            #重新加載配置文件
nmcli connection up ens192         #不重啟系統，讓網卡生效
nmcli                              #查看IP詳情

ip a

yum install epel-release wget net-tools vim telnet chrony
yum upgrade --refresh

hostnamectl set-hostname 改主機名.localdomain
```
```php
1 關閉selinux
vim /etc/selinux/config
SELINUX=disabled

2 rc.local 新增執行權限
echo '#!/bin/bash' > /etc/rc.d/rc.local 預設有了
chmod +x /etc/rc.d/rc.local

3 設定時間同步
vi /etc/chrony.conf
##pool 2.rocky.pool.ntp.org iburst
server <ip>
systemctl restart chronyd
systemctl enable chronyd

echo '0 * * * * root chronyc -a makestep &> /dev/null' >> /etc/crontab
echo 'chronyc -a makestep' >> /etc/rc.d/rc.local
###chronyc sources   檢查
```
```
nfs主機內文件要先登記要開放的目錄給哪些主機
vim /etc/exports
exportfs -arv




```
