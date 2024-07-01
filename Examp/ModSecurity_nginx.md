```
# ubuntu
apt install nginx
# rocky
yum install nginx
```
```
# ubuntu
apt-get install libtool autoconf build-essential libpcre3-dev zlib1g-dev libssl-dev libxml2-dev libgeoip-dev liblmdb-dev libyajl-dev libcurl4-openssl-dev libpcre++-dev pkgconf libxslt1-dev libgd-dev automake
# rocky
yum groupinstall -y "Development Tools"
yum install -y  httpd-devel pcre pcre-devel libxml2 libxml2-devel curl curl-devel openssl openssl-devel
```

```
# ubuntu  # rocky
cd /usr/local/src
git clone --depth 100 -b v3/master --single-branch https://github.com/SpiderLabs/ModSecurity
cd ModSecurity
git submodule init
git submodule update

# Generate configure file
sh build.sh
# Pre compilation step. Checks for dependencies
./configure
# Compiles the source code
make
# Installs the Libmodsecurity to **/usr/local/modsecurity/lib/libmodsecurity.so**
make install


nginx -V
```
Step 3. Download and Compile ModSecurity v3 Nginx Connector Source Code
```
# ubuntu  # rocky

mkdir /usr/local/src/cpg
cd /usr/local/src/cpg
#Make sure to change versoin number match it with your local Nginx server version
wget http://nginx.org/download/nginx-1.21.4.tar.gz
# Extract the downloaded source code...make sure to use the corerct Nginx version number that you have downloaded 
tar -xvzf nginx-1.21.4.tar.gz
# Download the source code for ModSecurity-nginx connector
git clone https://github.com/SpiderLabs/ModSecurity-nginx

```
```
# Compile the Nginx...make sure to use the corerct Nginx version number that you have downloaded 
cd nginx-1.21.4
./configure --with-compat --with-openssl=/usr/include/openssl/ --add-dynamic-module=/usr/local/src/cpg/ModSecurity-nginx
```
```
# Compile the Nginx...make sure to use the corerct Nginx version number that you have downloaded 
cd nginx-1.21.4
./configure --with-cc-opt='-g -O2 -fdebug-prefix-map=/home/clp/packaging/nginx/tmp/nginx-1.21.4=. -fstack-protector-strong -Wformat -Werror=format-security -fPIC -Wdate-time -D_FORTIFY_SOURCE=2' --with-ld-opt='-Wl,-z,relro -Wl,-z,now -fPIC' --prefix=/usr/share/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --lock-path=/var/lock/nginx.lock --pid-path=/run/nginx.pid --modules-path=/usr/lib/nginx/modules --http-client-body-temp-path=/var/lib/nginx/body --http-fastcgi-temp-path=/var/lib/nginx/fastcgi --http-proxy-temp-path=/var/lib/nginx/proxy --http-scgi-temp-path=/var/lib/nginx/scgi --http-uwsgi-temp-path=/var/lib/nginx/uwsgi --with-debug --with-pcre-jit --with-http_ssl_module --with-http_stub_status_module --with-http_realip_module --with-http_auth_request_module --with-http_v2_module --with-http_dav_module --with-http_slice_module --with-threads --with-http_addition_module --with-http_geoip_module=dynamic --with-http_gunzip_module --with-http_gzip_static_module --with-http_image_filter_module=dynamic --with-http_sub_module  --with-stream_ssl_module --with-stream_ssl_preread_module --with-mail=dynamic --with-mail_ssl_module  --add-dynamic-module=/usr/local/src/cpg/ModSecurity-nginx
```
```
# Generate the module
make modules
# Copy the module to the Nginx module directory
cp objs/ngx_http_modsecurity_module.so /usr/share/nginx/modules/

```
Step4. Load ModSecurity Module into Nginx
```
# ubuntu 
Open file /etc/nginx/modules-enabled/50-mod-http-modsecurity.conf and add the following contents
load_module modules/ngx_http_modsecurity_module.so;

# rocky
Open file /etc/nginx/mod-http-modsecurity.conf and add the following contents
load_module modules/ngx_http_modsecurity_module.so;
```
Step 5. Install Nginx configuration
```
ubuntu
###Open /etc/nginx/nginx.conf and add the following line after including “/etc/nginx/sites-enabled/*.conf”
include /etc/nginx/cpguard_waf_load.conf;

###Add the following contents to /etc/nginx/cpguard_waf_load.conf
modsecurity on;
modsecurity_rules_file /etc/nginx/nginx-modsecurity.conf;

###Add following contents to /etc/nginx/nginx-modsecurity.conf
SecRuleEngine On
SecRequestBodyAccess On
SecDefaultAction "phase:2,deny,log,status:406"
SecRequestBodyLimitAction ProcessPartial
SecResponseBodyLimitAction ProcessPartial
SecRequestBodyLimit 13107200
SecRequestBodyNoFilesLimit 131072
SecPcreMatchLimit 250000
SecPcreMatchLimitRecursion 250000
SecCollectionTimeout 600
SecDebugLog /var/log/nginx/modsec_debug.log
SecDebugLogLevel 0
SecAuditEngine RelevantOnly
SecAuditLog /var/log/nginx/modsec_audit.log
SecUploadDir /tmp
SecTmpDir /tmp
SecDataDir /tmp
SecTmpSaveUploadedFiles on
# Include file for cPGuard WAF
Include /etc/nginx/cpguard_waf.conf
```
Step 5. Install Nginx configuration
```
rocky
###Open /etc/nginx/conf.d/nginx_modsec.conf and add the following line into it.
modsecurity on;
modsecurity_rules_file /etc/nginx/cpguard-modsecurity.conf;

###2. Add the following contents to /etc/nginx/cpguard-modsecurity.conf
SecRuleEngine On
SecRequestBodyAccess On
SecDefaultAction "phase:2,deny,log,status:406"
SecRequestBodyLimitAction ProcessPartial
SecResponseBodyLimitAction ProcessPartial
SecRequestBodyLimit 13107200
SecRequestBodyNoFilesLimit 131072
SecPcreMatchLimit 250000
SecPcreMatchLimitRecursion 250000
SecCollectionTimeout 600
SecDebugLog /var/log/nginx/modsec_debug.log
SecDebugLogLevel 0
SecAuditEngine RelevantOnly
SecAuditLog /var/log/nginx/modsec_audit.log
SecUploadDir /tmp
SecTmpDir /tmp
SecDataDir /tmp
SecTmpSaveUploadedFiles on
# Include file for cPGuard WAF
Include /etc/nginx/cpguard_waf.conf

```
```
waf_server = nginx
waf_server_conf = /etc/nginx/cpguard_waf.conf
waf_server_restart_cmd = /usr/sbin/service nginx restart
waf_audit_log = /var/log/nginx/modsec_audit.log
```
https://opsshield.com/help/cpguard/category/waf/
