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

5. 連線閒置時間

```jsx
我設定是
vim /etc/ssh/sshd_config
PermitRootLogin no
ClientAliveInterval 900
ClientAliveCountMax 0
```

6 root 閒置登出

```jsx
vim /etc/profile   
export TMOUT=1800
source /etc/profile  --使剛才修改的配置文件立即生效
```
```
7 logrotate 檔案分割
vi /etc/logrotate.conf

daily
rotate 90

```
```
vi /etc/sysctl.conf
# sysctl settings are defined through files in
# /usr/lib/sysctl.d/, /run/sysctl.d/, and /etc/sysctl.d/.
#
# Vendors settings live in /usr/lib/sysctl.d/.
# To override a whole file, create a new file with the same in
# /etc/sysctl.d/ and put new settings there. To override
# only specific settings, add a file with a lexically later
# name in /etc/sysctl.d/ and put new settings there.
#
# For more information, see sysctl.conf(5) and sysctl.d(5).
net.ipv4.tcp_timestamps=0

# Increase size of file handles and inode cache
fs.file-max = 81920000
fs.nr_open = 81920000

# Do less swapping
vm.swappiness = 10
vm.dirty_ratio = 60
vm.dirty_background_ratio = 2

### GENERAL NETWORK SECURITY OPTIONS ###

# Number of times SYNACKs for passive TCP connection.
net.ipv4.tcp_synack_retries = 2

# Allowed local port range
net.ipv4.ip_local_port_range = 2000 65535

# Protect Against TCP Time-Wait
net.ipv4.tcp_rfc1337 = 1

# Decrease the time default value for tcp_fin_timeout connection
net.ipv4.tcp_fin_timeout = 15

# Decrease the time default value for connections to keep alive
net.ipv4.tcp_keepalive_time = 300
net.ipv4.tcp_keepalive_probes = 5
net.ipv4.tcp_keepalive_intvl = 15

### TUNING NETWORK PERFORMANCE ###

# Default Socket Receive Buffer
net.core.rmem_default = 31457280

# Maximum Socket Receive Buffer
net.core.rmem_max = 12582912

# Default Socket Send Buffer
net.core.wmem_default = 31457280

# Maximum Socket Send Buffer
net.core.wmem_max = 12582912

# Increase number of incoming connections
net.core.somaxconn = 65536

# Increase number of incoming connections backlog
net.core.netdev_max_backlog = 65536

# Increase the maximum amount of option memory buffers
net.core.optmem_max = 25165824

# Increase the maximum total buffer-space allocatable
# This is measured in units of pages (4096 bytes)
net.ipv4.tcp_mem = 65536 131072 262144
net.ipv4.udp_mem = 65536 131072 262144

# Increase the read-buffer space allocatable
net.ipv4.tcp_rmem = 8192 87380 16777216
net.ipv4.udp_rmem_min = 16384

# Increase the write-buffer-space allocatable
net.ipv4.tcp_wmem = 8192 65536 16777216
net.ipv4.udp_wmem_min = 16384

# Increase the tcp-time-wait buckets pool size to prevent simple DOS attacks
net.ipv4.tcp_max_tw_buckets = 1440000
net.ipv4.tcp_tw_recycle = 1
net.ipv4.tcp_tw_reuse = 1

#我新增設定檔
# Disable ipv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1

net.netfilter.nf_conntrack_max=1048576
net.netfilter.nf_conntrack_tcp_timeout_established=300
net.netfilter.nf_conntrack_buckets=262144
```
