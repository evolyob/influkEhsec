```php
# 防火牆政策+iptables

vim /etc/firewalld/zones/public.xml


<?xml version="1.0" encoding="utf-8"?>
<zone>
  <short>Public</short>
  <description>For use in public areas. You do not trust the other computers on networks to not harm your computer. Only selected incoming connections are accepted.</description>
  <service name="dhcpv6-client"/>
注意---------------------------------->  <service name="ssh"/>   #刪除 ssh All
  <service name="cockpit"/>
  <forward/>

新增  
<rule family="ipv4">
    <source address="**.***.***.0/24"/>   #允許VPN的IP SSH登入
    <service name="ssh"/>
    <accept/>
</rule>
<rule family="ipv4">
    <source address="**.**.**.***/29"/>    #允許機房的**網段NB SSH登入
    <accept/>
</rule>

<rule family="ipv4">
    <source address="172.**.***.***/32"/>  
    <accept/>
</rule>
<rule family="ipv4">
    <source address="172.**.***.***/24"/>   #允許同vlan
    <accept/>
</rule>

</zone>

```
```php
開防火牆服務

#新增https 
firewall-cmd --permanent --zone=public --add-service=https

#新增 zabbix監控
firewall-cmd --permanent --add-port=10050/tcp

##dns
firewall-cmd --reload

firewall-cmd --list-all
```








