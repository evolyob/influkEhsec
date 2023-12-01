#### NTP server Ver.
 ```
  #chronyd -v
  #timedatectl 
  #cat /etc/chrony.conf
  #chronyc tracking
```
#### TCP/UDP port list
```
  #netstat -ntul
```
#### OSSEC ver.
```
  #/var/ossec/bin/ossec-analysisd -V
  #/var/ossec/etc/ossec.conf
```
#### LogServer ver.
```
  #/usr/sbin/rsyslogd -v
```
#### ClamAV
```
  #systemctl status clamav-freshclam.service
  #clamscan --version
```
#### VM root list
 ``` 
  #cat /etc/passwd
  #cat /etc/group
```
#### VM Updates 
```
  #yum history
```

#### VM enable server list
```
  #systemctl list-unit-files | egrep 'service|enabled'
```

```
網卡  
##centos
cat /etc/sysconfig/network-scripts/ifcfg-ens192

##Rocky Linux
cat /etc/NetworkManager/system-connections/ens32.nmconnection

cat /etc/hosts
cat /etc/firewalld/zones/public.xml
cat /etc/sudoers


```
