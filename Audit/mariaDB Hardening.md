```php
>>Disable Command History
path:/root/.mysql_history.
  #find /home -name ".mysql_history"
  #find /root -name ".mysql_history"
Remediation:
  - Remove .mysql_history
  - # > ln -s /dev/null $HOME/.mysql_history
```
```php
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
```
>Lock Out Accounts if Not Currently in Use
```php
Remediation:
To lock accounts - example:
ALTER USER 'jeffrey'@'localhost' ACCOUNT LOCK;
To unlock accounts - example
ALTER USER 'jeffrey'@'localhost' ACCOUNT UNLOCK;
SET PERSIST slow_query_log = OFF;
SET PERSIST @@GENERAL_LOG=OFF;
```
>Harden Usage for 'local_infile' on MariaDB Clients
```php
$ mariadb --version
const char *mysql_get_client_info(void)
SHOW VARIABLES WHERE Variable_name = 'local_infile';

mariadb --local-infile=0 --load-data-local-dir=/my/local/data
mariadb --local-infile=0 --load-data-local-dir=/my/local/data --ssl-mode=VERIFY_IDENTITY
local-infile=0


SELECT VARIABLE_NAME, VARIABLE_VALUE
FROM information_schema.global_variables
WHERE VARIABLE_NAME = 'ssl_cipher';
Set ssl_cipher to one or more approved cipher suites in your MariaDB configuration file, then restart MariaDB.
ssl_cipher='ECDHE-ECDSA-AES128-GCM-SHA256'

>Create the key file:
sudo mkdir -p /etc/mysql/encryption && (echo -n "1;" ; openssl rand -hex 32 ) | sudo tee -a /etc/mysql/encryption/keyfile
sudo openssl rand -hex 128 | sudo tee -a /etc/mysql/encryption/keyfile.key
>Generate a random encryption password:
sudo openssl rand -hex 128 | sudo tee -a /etc/mysql/encryption/keyfile.key
>Encrypt the key file:
$ sudo openssl enc -aes-256-cbc -md sha1 \ -pass file:/etc/mysql/encryption/keyfile.key \ -in /etc/mysql/encryption/keyfile \ -out /etc/mysql/encryption/keyfile.enc
>Delete the unencrypted key file:
sudo rm /etc/mysql/encryption/keyfile
>Set permissions and ownership on the keyfile and key:
$ sudo chown mysql:mysql -R /etc/mysql/encryption
$ sudo chmod 640 /etc/mysql/encryption/keyfile*
```
>Edit mariadb.cnf to resemble the following block, optionally uncommenting
```
file_key_management_encryption_algorithm = AES_CTR:
[mariadb] ... plugin_load_add = file_key_management
file_key_management_filename = /etc/mysql/encryption/keyfile.enc
file_key_management_filekey = FILE:/etc/mysql/encryption/keyfile.key
# Binary Log Encryption
encrypt_binlog = ON
# Redo Log Encryption
innodb_encrypt_log = ON
# Encrypting Temporary Files
encrypt_tmp_files = ON
# You can configure InnoDB encryption to automatically have all new InnoDB tables automatically encrypted, or specify encrypt per table. innodb_encrypt_tables = ON
# Uncomment the line below if utilizing MariaDB built with OpenSSL
# file_key_management_encryption_algorithm = AES_CTR

systemctl restart mariadb.service
ALTER TABLE tab1 ENCRYPTED=YES ENCRYPTION_KEY_ID=1;
```
>Ensure mariadb is Not Started With 'skip-grant-tables'
```php
e.g., mariadb.cnf
skip-grant-tables = FALSE
If there are any occurrences of skip_grant_tables, also set that to FALSE or remove
```
