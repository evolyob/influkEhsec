```
#啟用設定
sysctl -p /etc/sysctl.conf

#檢查是否生效
sysctl -a

#重新載入
sysctl -p
```
```
net.ipv4.tcp_timestamps=0

# Number of times SYNACKs for passive TCP connection.
net.ipv4.tcp_synack_retries = 2

# Allowed local port range
net.ipv4.ip_local_port_range = 2000 65535

# Protect Against TCP Time-Wait
net.ipv4.tcp_rfc1337 = 1

# Decrease the time default value for tcp_fin_timeout connection
net.ipv4.tcp_fin_timeout = 15

# Decrease the time default value for connections to keep alive
 net.ipv4.tcp_keepalive_time = 3600
 net.ipv4.tcp_keepalive_probes = 5
 net.ipv4.tcp_keepalive_intvl = 30

# Increase the tcp-time-wait buckets pool size to prevent simple DOS attacks
net.ipv4.tcp_max_tw_buckets = 1440000
net.ipv4.tcp_tw_reuse = 1

# Disable ipv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1


### TUNING NETWORK PERFORMANCE ###

# Default Socket Receive Buffer
# net.core.rmem_default = 31457280

# Maximum Socket Receive Buffer
# net.core.rmem_max = 12582912

# Default Socket Send Buffer
# net.core.wmem_default = 31457280

# Maximum Socket Send Buffer
# net.core.wmem_max = 12582912

# Increase number of incoming connections
# net.core.somaxconn = 65536

# Increase number of incoming connections backlog
# net.core.netdev_max_backlog = 65536

# Increase the maximum amount of option memory buffers
# net.core.optmem_max = 25165824

# Increase the maximum total buffer-space allocatable
# This is measured in units of pages (4096 bytes)
# net.ipv4.tcp_mem = 65536 131072 262144
# net.ipv4.udp_mem = 65536 131072 262144

# Increase the read-buffer space allocatable
# net.ipv4.tcp_rmem = 8192 87380 16777216
# net.ipv4.udp_rmem_min = 16384

# Increase the write-buffer-space allocatable
# net.ipv4.tcp_wmem = 8192 65536 16777216
# net.ipv4.udp_wmem_min = 16384
```
```
sysctl -p
```

```
net.ipv4.tcp_timestamps = 0
net.ipv4.tcp_synack_retries = 2
net.ipv4.ip_local_port_range = 2000 65535
net.ipv4.tcp_rfc1337 = 1
net.ipv4.tcp_fin_timeout = 15
net.ipv4.tcp_keepalive_time = 3600
net.ipv4.tcp_keepalive_probes = 5
net.ipv4.tcp_keepalive_intvl = 30
net.ipv4.tcp_max_tw_buckets = 1440000
net.ipv4.tcp_tw_reuse = 1
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
```

NTP
```
apt install chrony

vi /etc/chrony/chrony.conf
#pool ntp.ubuntu.com        iburst maxsources 4

server <ip> iburst

```
```
systemctl stutas chronyd
systemctl restart chronyd
systemctl enable chronyd
```

帳號90天換密碼
```
vim /etc/login.defs
PASS_MAX_DAYS   90
```
```
連線閒置時間
vim /etc/ssh/sshd_config

PermitRootLogin no
122
ClientAliveInterval 900
ClientAliveCountMax 0

## 最後一行加上  #允許ssh 登入帳號
AllowUsers
```
```
systemctl restart sshd
```

```
logrotate 檔案分割 設定 以"日"  90天或30天存檔

vim /etc/logrotate.conf

#weekly
daily
rotate 30

###重整
logrotate -f /etc/logrotate.conf
```

```
# 改hostname名稱

vim /etc/hostname
```



