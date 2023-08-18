
### Network Security Control 
***
```php
Production VM Audit      $TRA__ 
Developer Traning            __ 
Backup Audit                 __
Log audit and monitor    $TRA__ 
Wireless Scan                __ 
ISMS Review                  __ 
end of live                  __
Intra VA                 $TRA__
ASV                      $TRA__ 
Intra PT                     __ 
Exter PT                     __ 
FIM check                    __ 
HTTP Header Check        $TRA__ 
IRP Drill                $TRA__
````

### Backup
```php
|Code|production        1/realTime|
|Code|synology /var,log 1/preDay  |
|Code|OA site  gitlab   1/realTime|
|Code|OA site  jumpVM   1/realTime|
```
```php
| DB |production        1/realTime|
| DB |synology   tables 4/preDay  |
| DB |OA siteDontHaveIt 0/day     |
```
```php
|Conf|SSHkey ForAPServer ifChange |
|Conf|FW PolicyRules     ifChange |
|Conf|FW FortiToken      ifChange |
|Conf|VM ESXiServers     ifChange |
|Conf|Web SSLCSR+CA      ifChange |
```


### Monitor VM status
```
|  ELK  |SSHFail,CheckSum,APLog,Others.... |realtime|
```
```
| OSSEC |SSHFail,CheckSum,UpdatesErr,Others|realtime|
|Zabbix |ActiveStatus,CPUlaod,DiskSpace,etc|realtime|
|MDR_01 | Endpoint   SomebodyDontKnow      |realtime|
|  SOC  | FW AV IPS WAF L34567             |realtime|
|Cleaner| WhenDDOShappenToWebsiteFlow      |realtime|
```

### TechSolution

- [ ] 1. prevent/ban copy or relocation of PAN when remote-access
// 
- [ ] 2. anti-malware scans when removeable electronic media is in use 
// 
- [ ] 3. detect and protect personnel against phishing attacks
// 
- [ ] 4. web application that continually detects and prevents wed-based attacks
// 
- [ ] 5. payment pagescript that are load excue in consumers 
// 
- [ ] 6. audit log review are automated

- [ ] 7. failures detected alerted and addressed promptly
// 
- [ ] 8. intra VA use authentication scaning
// 
- [ ] 9. IDS/IPS able detect/monitor bypass Attck(DNS tunneling,CC...)
// 
- [ ] 10.change/tamper/detection mechanism is deployed
// 
