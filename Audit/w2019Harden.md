Windows Server 2019  v2.0.0 - 04-14-2023
```php
**Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\
Enforce password history                      >>> 24 or more password
Maximum password age                          >>> 365 or fewer days, but not 0
Minimum password age'                         >>> 1 or more 
Minimum password length                       >>> 14 or more 
Password must meet complexity requirements    >>> Enabled
Store passwords using reversible encryption   >>> Disable

**Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy\
Account lockout duration                      >>> 15 or more
Account lockout threshold                     >>>  5 or fewer , but not 0
Allow Administrator account lockout           >>> Enabled 
Reset account lockout counter after           >>> 15 or more
```
```php
**Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\
Access Credential Manager as a trusted caller   >>> No One
Access this computer from the network           >>> Administrators, Authenticated Users 
Act as part of the operating system             >>> No One
Add workstations to domain                      >>> Administrators ??
Adjust memory quotas for a process              >>> Administrators, LOCAL SERVICE, NETWORK SERVICE
Allow log on locally                            >>> Administrators
Assignment\Allow log on through Remote Desktop Services  >>> Administrators
Allow log on through Remote Desktop Services    >>> Administrators, Remote Desktop Users
Back up files and directories                   >>> Administrators

Change the system time                          >>> Administrators, LOCAL SERVICE,
Change the time zone                            >>> Administrators, LOCAL SERVICE,
Create a pagefile                               >>> Administrators
Create a token object                           >>> No One
Create global objects                           >>> Administrators, LOCAL SERVICE, NETWORK SERVICE, SERVICE
Create permanent shared objects                 >>> No One
Create symbolic links                           >>> Administrators, Virtual Machines

Debug programs                                  >>> Administrators
Deny access to this computer from the network   >>> Guests, Local account and member of Administrators group
Deny log on as a batch job                      >>> Guests
Deny log on as a service                        >>> Guests
Deny log on locally                             >>> Guests
Deny log on through Remote Desktop Services     >>> Guests, Local account

Enable computer and user accounts to be trusted for delegation  >>> Administrators
Force shutdown from a remote system             >>> Administrators
Generate security audits              `         >>>LOCAL SERVICE, NETWORK SERVICE
Impersonate a client after authentication       >>>Administrators, LOCAL SERVICE, NETWORK SERVICE, SERVICE.
Increase scheduling priority                    >>> Administrators, Window Manager\Window Manager Group: 
Load and unload device drivers                  >>> Administrators
Lock pages in memory                            >>> No One
Log on as a batch job                           >>> Administrators

Modify an object label                          >>> No One
Modify firmware environment values              >>> Administrators
Perform volume maintenance tasks                >>> Administrators
Profile single process                          >>> Administrators
Replace a process level token                   >>> LOCAL SERVICE, NETWORK SERVICE
Restore files and directories                   >>> Administrators
Shut down the system                            >>> Administrators
Take ownership of files or other objects        >>> Administrators

Active Directory
Synchronize directory service data             >>> No One

```
### Security Options
```php
***Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\
Accounts: Block Microsoft accounts             >>> Users can't add or log on with Microsoft accounts
Accounts: Guest account status                 >>> Disabled











```
