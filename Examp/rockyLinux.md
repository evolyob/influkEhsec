
```php
chk vm tool
#vmware-toolbox-cmd -v

#dnf install open-vm-tools vim telnet net-tools rsync
#rebot
#yum update
```
```php
disable selinux
#vim /etc/selinux/config
#SELINUX=enforcing
SELINUX=disabled
#rebot
```
```php
#換網卡UUID
#也可在網卡內把UUID設定#掉，不影響現行環境

uuidgen ens192   #產一組新的UUID，複製起來，等等進網卡設定內貼上
nmcli connection reload            #重新加載配置文件
nmcli connection up ens192         #不重啟系統，讓網卡生效
nmcli                              #查看IP詳情

vim /etc/NetworkManager/system-connections/ens32.nmconnection

systemctl restart NetworkManager   #重啟網卡
```
```php
#換系統的Machine ID
hostnamectl					#顯示系統資訊
rm /etc/machine-id			#移除ID，跳出確認訊息按 y 同意
systemd-machine-id-setup	#重新產生ID
hostnamectl					#再次顯示系統資訊
```
```
# 加執行權限
cd /etc/rc.d
chmod +x /etc/rc.d/rc.local
```
```php
# 整點檢查時間同步
yum install chrony
vim /etc/chrony.conf
server <ip> iburst          

systemctl restart chronyd
systemctl enable chronyd

vim /etc/crontab
echo '0 * * * * root chronyc -a makestep ' >> /etc/crontab

vim /etc/rc.d/rc.local
echo 'chronyc -a makestep' >> /etc/rc.d/rc.local

###檢查 命令如下
chronyc -a makestep   \\200 OK
chronyc tracking
chronyc sources  
```
```php
密碼原則
echo 'minlen=12' >> /etc/security/pwquality.conf
echo 'dcredit=-1' >> /etc/security/pwquality.conf
echo 'ucredit=-1' >> /etc/security/pwquality.conf
echo 'lcredit=-1' >> /etc/security/pwquality.conf
#ucredit=-1: upper-case 大寫字母最少 1 個
#lcredit=-2: lower-case 小寫字母最少 2 個
#dcredit=-3: digit-case 數字字母最少 3 個
#ocredit=-4: other-case 其他字母最少 4 個

#簡易做法
vim  /etc/security/pwquality.conf  最後面加
minlen=12
dcredit=-1
ucredit=-1
lcredit=-1

帳號90天換密碼
###改設定檔
vim /etc/login.defs
39
PASS_MAX_DAYS   90

###或是之後另外再調整 
vim /etc/shadow

###或是改指定帳號
passwd -x 90 mis01
```
```php
連線閒置時間

vim /etc/ssh/sshd_config
44
PermitRootLogin no
122
ClientAliveInterval 900
ClientAliveCountMax 0

最後一行加上  #允許ssh 登入帳號
AllowUsers <a><b><c>

systemctl restart sshd

 root 閒置登出
vim /etc/profile
export TMOUT=1800

source /etc/profile  --使剛才修改的配置文件立即生效
```
```php
# logrotate 檔案分割 設定 以"日"

vim /etc/logrotate.conf
#weekly
daily
rotate 30

logrotate -f /etc/logrotate.conf
```
```php
網卡效能設定
vim /etc/sysctl.conf
增加
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

#啟用設定
sysctl -p /etc/sysctl.conf

#檢查是否生效
sysctl -a

#重新載入
sysctl -p
```
```php
# ulimit

vim /etc/security/limits.conf
最後面一行新增加上

*         hard    nofile      5000000
*         soft    nofile      5000000
root      hard    nofile      5000000
root      soft    nofile      5000000
*         hard    nproc       5000000
*         soft    nproc       5000000
*         hard    sigpending  5000000
*         soft    sigpending  5000000
*         hard    memlock     8192
*         soft    memlock     8192
*         hard    stack       8192
*         soft    stack       8192

##下面兩個 File 能加到5百萬
##能調低沒關係 但最好跟  limits.conf 對照

vim /etc/systemd/system.conf

最後面一行新增加上
DefaultTasksMax=512000
DefaultLimitNOFILE=5000000
DefaultLimitNPROC=5000000

vim /etc/systemd/user.conf

最後面一行新增加上
DefaultLimitNOFILE=5000000
DefaultLimitNPROC=5000000


重啟、檢查ulimit
reboot
ulimit -a
```
```php
user sudo 帳號權限
vim /etc/sudoers

root    ALL=(ALL)       ALL
#100 新增
mis01   ALL=(ALL)       ALL
```
```php
要mount的系統都要安裝mount套件
dnf install nfs-utils nfs4-acl-tools

檢查mount設備是否可以連線
showmount -e IP

設定rc.local設定檔
vim /etc/rc.d/rc.local
範例
	mount <ip>:/path
	#mount 來源 目的 
	#都設定mount在根目錄，所以要先在根目錄新增同名的目錄資料夾

再到指定目錄下
	cd /var/vhosts/www/storage/app/
	
ln連結相對應的目錄，不需新增目錄，不然會ln到目錄內	
	ln -sf /path ./public
	ll 				#檢查是否有ln成功，即可
```

```php



```

















