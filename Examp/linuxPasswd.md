#### VM passwd policy
```
  #vi /etc/pam.d/system-auth
```
```bash
#%PAM-1.0
# This file is auto-generated.
# User changes will be destroyed the next time authselect is run.
auth        required      pam_faillock.so preauth silent even_deny_root audit deny=5 unlock_time=1800
auth        sufficient    pam_unix.so nullok try_first_pass
auth        [default=die] pam_faillock.so  authfail even_deny_root  audit  deny=5  unlock_time=1800
auth        required      pam_env.so
auth        sufficient    pam_unix.so try_first_pass nullok
auth        required      pam_deny.so

account     required      pam_faillock.so
account     required      pam_unix.so

password    requisite     pam_pwquality.so try_first_pass local_users_only retry=3 authtok_type= minlen=15 lcredit=1 ucredit=1 dcredit=1 ocredit=0

password    sufficient    pam_unix.so try_first_pass use_authtok nullok sha512 shadow remember=4

password    required      pam_deny.so

session     optional      pam_keyinit.so revoke
session     required      pam_limits.so
-session     optional      pam_systemd.so
session     [success=1 default=ignore] pam_succeed_if.so service in crond quiet use_uid
session     required      pam_unix.so
```
