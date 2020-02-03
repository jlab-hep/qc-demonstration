---

# Advance : apache

The viewer can be accessed via apache. 

## 1) Configure apache2

   ```
   $ cd /var/www/localDB-tools
   $ sudo cp scripts/apache/config.conf /etc/httpd/conf.d/web-app-db-yarr.conf
   ```

   If you want to limit where to access the viewer, remove comment out and add `Allow from XXX`.

   For example, in case you allow access from `ac.jp`, you change the config file as below:
   ```
   <Proxy *>
       Order deny,allow
       Deny from all
       Allow from ac.jp
   #    Allow from all
   </Proxy>
   <Location /yarrdb/>
       Order deny,allow
       Deny from all
       Allow from ac.jp
   #    Allow from all
   </Location>
   <VirtualHost *:80>
     ProxyPreserveHost On
     ProxyRequests Off
     ProxyPass /yarrdb/ http://localhost:5000/yarrdb/
     ProxyPassReverse /yarrdb/ http://localhost:5000/yarrdb/
   </VirtualHost>
   ```

## 2) Allow httpd make network request
   This allows apache connect to mongo server
   ```
   $ sudo /usr/sbin/setsebool -P httpd_can_network_connect 1
   ```

## 3) Restart apache service
   ```
   $ sudo systemctl start httpd
   $ sudo systemctl enable httpd
   ```

## 4) Open 80 port if need
   ```
   sudo firewall-cmd --add-service=http --permanent
   sudo firewall-cmd --reload
   ```
