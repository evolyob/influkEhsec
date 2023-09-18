```php
>>Disable Command History
path:/root/.mysql_history.
  #find /home -name ".mysql_history"
  #find /root -name ".mysql_history"
Remediation:
  - Remove .mysql_history
  - # > ln -s /dev/null $HOME/.mysql_history

>> Backups Should be Properly Secured
  -The example above creates an AES-encrypted backup, protected with the password "mypass" and stores it in a file "backup.xb.enc":
#$ mariabackup --defaults-file=/home/dbadmin/my.cnf --backup --stream=xbstream \ | openssl enc -aes-256-cbc -k mypass > backup.xb.enc

>>Point-in-Time Recovery
 - Check if binlogs are enabled and if there is a restore procedure
  #--binlog-expire-logs-second
  #SELECT VARIABLE_NAME, VARIABLE_VALUE, 'BINLOG - Log Expiration' as Note FROM information_schema.global_variables where variable_name = 'binlog_expire_logs_seconds';
$$$$     value is not set to 0.
****Default Value  :  binlog-expire-logs-seconds  = 864000 seconds, or 10 days.


>>Backup of Configuration and Related Files
- Edited Configuration files (mariadb.cnf and included files)
- a properly secured .mariadb.cnf file, or store authentication information in encrypted format in .mylogin.cnf.

>>Ensure 'password_lifetime' is Less Than or Equal to '365'
SET GLOBAL default_password_lifetime=365;
ALTER USER '<username>'@'<localhost>' PASSWORD EXPIRE INTERVAL 365 DAY;
*****Default Value:NULL

>>>Lock Out Accounts if Not Currently in Use
Remediation:
To lock accounts - example:
ALTER USER 'jeffrey'@'localhost' ACCOUNT LOCK;
To unlock accounts - example
ALTER USER 'jeffrey'@'localhost' ACCOUNT UNLOCK;


```
