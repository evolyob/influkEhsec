FW conf.d
```
- passwd,usr list, ver.
- access cipher mode, routing table
- wan -> dmz,  dmz -> intr
- intr-->dmz,  dmz-->wan
- anit-spoofing, NAT conf , log conf, NTP
```
DNS conf.d
```php
- DNS ver.
#dnf list installed bind
#netstat -ntul
- DNS root, 2log Serer
```
NTP conf.d
```php
#chronyd -v
#timedatectl
-2log Serer
# cat /etc/chrony.conf
```
LogServer conf.d
```php
- passwd policy and list
# cat/etc/group
# /usr/sbin/rsyslogd -v
- log monitor >> elk、mdr
```
Anti-Virus conf.d
```php
# clamscan --version
crontab scan and update
#cat /etc/crontab
```
LinuxHardening
```php
#cat /etc/passwd
#cat /etc/group
#ssh -V
#/etc/ssh/sshd_config
#yum history
# vi  /etc/pam.d/sshd
#netstat -ltupn | grep LISTEN
#systemctl list-unit-files | egrep 'service|enabled'
#vi /etc/service  log agent ??
#chronyc tracking
#cat /etc/chrony.conf
```



