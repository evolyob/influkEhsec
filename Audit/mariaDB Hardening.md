```php
>>Disable Command History
path:/root/.mysql_history.
  #find /home -name ".mysql_history"
  #find /root -name ".mysql_history"
Remediation:
  - Remove .mysql_history
  - # > ln -s /dev/null $HOME/.mysql_history

>>MYSQL_PWD Environment Variable is Not in Use
  #grep MYSQL_PWD /proc/*/environ

```
