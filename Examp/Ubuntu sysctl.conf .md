```php
#啟用設定
sysctl -p /etc/sysctl.conf

#檢查是否生效
sysctl -a

#重新載入
sysctl -p
```
```php
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

```php
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
```php
apt install chrony
# systemctl stop systemd-timesyncd.service
# systemctl mask systemd-timesyncd.service

vi /etc/chrony/chrony.conf
#pool ntp.ubuntu.com        iburst maxsources 4

server <ip> iburst

```
```php
systemctl stutas chrony
systemctl restart chrony
systemctl enable chrony
chronyc sources -v
```

帳號90天換密碼
```php
vim /etc/login.defs
# login.defs無法檢查密碼複雜度
PASS_MAX_DAYS   180
PASS_MIN_DAYS 1
```
```php
連線閒置時間
vim /etc/ssh/sshd_config

PermitRootLogin no

ClientAliveInterval 900
ClientAliveCountMax 0

## 最後一行加上  #允許ssh 登入帳號
AllowUsers
```
```
systemctl restart sshd
```

```php
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
```php
apt install libpam-pwquality
vi /etc/security/faillock.conf
deny = 5
unlock_time = 900

```
```php
vi /etc/security/pwquality.conf

# Configuration for systemwide password quality limits
# Defaults:
#
# Number of characters in the new password that must not be present in the
# old password.
difok = 2

# Minimum acceptable size for the new password (plus one if
# credits are not disabled which is the default). (See pam_cracklib manual.)
# Cannot be set to lower value than 6.
minlen = 14
# The maximum credit for having digits in the new password. If less than 0
# it is the minimum number of digits in the new password.
dcredit = -1
# The maximum credit for having uppercase characters in the new password.
# If less than 0 it is the minimum number of uppercase characters in the new
# password.
ucredit = -1
# The maximum credit for having lowercase characters in the new password.
# If less than 0 it is the minimum number of lowercase characters in the new
# password.
lcredit = -1
# The maximum credit for having other characters in the new password.
# If less than 0 it is the minimum number of other characters in the new
# password.
# ocredit = 0
#
# The minimum number of required classes of characters for the new
# password (digits, uppercase, lowercase, others).
minclass = 3
# The maximum number of allowed consecutive same characters in the new password.
# The check is disabled if the value is 0.
maxrepeat = 3
# The maximum number of allowed consecutive characters of the same class in the
# new password.
# The check is disabled if the value is 0.
# maxclassrepeat = 0
#
# Whether to check for the words from the passwd entry GECOS string of the user.
# The check is enabled if the value is not 0.
# gecoscheck = 0
#
# Whether to check for the words from the cracklib dictionary.
# The check is enabled if the value is not 0.
dictcheck = 0
# Whether to check if it contains the user name in some form.
# The check is enabled if the value is not 0.
# usercheck = 1
#
# Length of substrings from the username to check for in the password
# The check is enabled if the value is greater than 0 and usercheck is enabled.
# usersubstr = 0
#
# Whether the check is enforced by the PAM module and possibly other
# applications.
# The new password is rejected if it fails the check and the value is not 0.
enforcing = 0
# Path to the cracklib dictionaries. Default is to use the cracklib default.
# dictpath =
#
# Prompt user at most N times before returning with error. The default is 1.
retry = 5
#
# Enforces pwquality checks on the root user password.
# Enabled if the option is present.
# enforce_for_root
#
# Skip testing the password quality for users that are not present in the
# /etc/passwd file.
# Enabled if the option is present.
# local_users_only
```
```
vi /etc/pam.d/common-password

```

```php
# Set Password Creation Requirement Parameters Using pam_cracklib
password    required            pam_cracklib.so retry=3 minlen=14 dcredit=-1 ucredit=-1 ocredit=-1 lcredit=-1

# Limit Password Reuse
password    sufficient          pam_unix.so remember=5
# here are the per-package modules (the "Primary" block)
password        requisite                       pam_pwquality.so retry=5
#password        [success=1 default=ignore]      pam_unix.so obscure use_authtok try_first_pass yescrypt
password        	[success=2 default=ignore]	     pam_unix.so obscure use_authtok try_first_pass sha512
# here's the fallback if no module succeeds
password        requisite                       pam_deny.so
# prime the stack with a positive return value if there isn't one already;
# this avoids us returning an error just because nothing sets a success code
# since the modules above will each just jump around
password        required                        pam_permit.so
# and here are more per-package modules (the "Additional" block)
# end of pam-auth-update config

```
```php
 /etc/systemd/journald.conf


# Entries in this file show the compile time defaults. Local configuration
# should be created by either modifying this file, or by creating "drop-ins" in
# the journald.conf.d/ subdirectory. The latter is generally recommended.
# Defaults can be restored by simply deleting this file and all drop-ins.
#
# Use 'systemd-analyze cat-config systemd/journald.conf' to display the full config.
#
# See journald.conf(5) for details.

[Journal]
Storage=persistent
#Compress=yes
#Seal=yes
#SplitMode=uid
#SyncIntervalSec=5m
#RateLimitIntervalSec=30s
#RateLimitBurst=10000
#SystemMaxUse=
#SystemKeepFree=
#SystemMaxFileSize=
#SystemMaxFiles=100
#RuntimeMaxUse=
#RuntimeKeepFree=
#RuntimeMaxFileSize=
#RuntimeMaxFiles=100
#MaxRetentionSec=
#MaxFileSec=1month
ForwardToSyslog=no
#ForwardToKMsg=no
#ForwardToConsole=no
#ForwardToWall=yes
#TTYPath=/dev/console
#MaxLevelStore=debug
#MaxLevelSyslog=debug
#MaxLevelKMsg=notice
#MaxLevelConsole=info
#MaxLevelWall=emerg
#LineMax=48K
#ReadKMsg=yes
#Audit=no
```

```php
#修改 PAM 設定以報告登入失敗
vi  /etc/pam.d/common-auth

# pam-auth-update(8) for details.

# here are the per-package modules (the "Primary" block)
auth    [success=1 default=ignore]      pam_unix.so nullok
######
auth	   [success=1 default=ignore]	     pam_exec.so quiet /usr/libexec/defender_iot_micro_agent/pam/pam_audit.sh 2
auth	   [success=1 default=ignore]	     pam_echo.so
# here's the fallback if no module succeeds
auth    requisite                       pam_deny.so

```
