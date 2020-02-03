# What is it?
A master server is a public server to communication between your lab and outside. Be careful everything and think again WHAT YOU ARE DOING when you follow this article.

## READ BEFORE CREATE A MASTER SERVER
https://www.mongodb.com/blog/post/mongodb-security-part-ii-10-mistakes-that-can



# Users Authentication

## Ready
As a administrator, 

### Create a new role
```
use admin
db.createRole(
   { role: "changeOwnPasswordCustomDataRole",
     privileges: [
        {
          resource: { db: "", collection: ""},
          actions: [ "changeOwnPassword", "changeOwnCustomData" ]
        }
     ],
     roles: []
   }
)
```

### Create an administrator user
```
use admin
db.createUser(
  {
    user: "adminuser",
    pwd: "adminpassword",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
```

### Create a normal user
* Read and Write privilege
```
use localdb
db.createUser(
   {
     user: "username",
     pwd: "userpassword",
     roles: [ "readWrite", { role:"changeOwnPasswordCustomDataRole", db:"admin" } ]
   }
)
```

* Read only privilege
```
use localdb
db.createUser(
   {
     user: "username",
     pwd: "userpassword",
     roles: [ "read", { role:"changeOwnPasswordCustomDataRole", db:"admin" } ]
   }
)
```

## Start a mongo server with authentication
Add below in the configuration file,
```
security:
    authorization: enabled
```
then restart the mongo server.
```
systemctl restart mongod.service
```

or add `--auth` when you type `mongodb`


## Login
### Connect
`mongo --host "your master server ip" --port 27017 -u "your user name" --authenticationDatabase 'localdb' -p`

then, input password

### Change password
```
use localdb
db.updateUser(
   "username",
   {
      pwd: "KNlZmiaNUp0B"
   }
)
```

Reference.
[Change Your Password and Custom Data](https://docs.mongodb.com/manual/tutorial/change-own-password-and-custom-data/)






# TSL/SSL
 
## Create certification and key
### for root
```
sudo openssl genrsa -out rootCA.key 2048
sudo openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem -subj "/C=JP/ST=Tokyo/L=Tokyo/O=root/OU=ITk/CN=192.168.1.32/emailAddress=<root-email>"
```


### for mongodb
```
sudo openssl genrsa -out mongodb.key 2048
sudo openssl req -new -key mongodb.key -out mongodb.csr -subj "/C=JP/ST=Tokyo/L=Tokyo/O=mongodb/OU=ITk/CN=192.168.1.32/emailAddress=<mongodb-email>"
```

CN(common-name) should be your bound IP address. e.g. 192.168.1.32


## x509 sign
```
sudo openssl x509 -req -in mongodb.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out mongodb.crt -days 500 -sha256
sudo cat mongodb.key mongodb.crt > mongodb.pem
```

## Copy files
```
sudo cp mongodb.pem /etc/ssl/mongodb.pem
sudo cp rootCA.pem /etc/ssl/ca.pem
```

## Enable TLS/SSL
in /etc/mongod.conf, add tls setting like below:
```
net:
  tls:
    mode: requireTLS
    certificateKeyFile: /etc/ssl/mongodb.pem
    CAFile: /etc/ssl/ca.pem
```
Caution: ssl is deprecated in mongodb. use tls instead. 

Restart server
```
sudo systemctl restart mongod.service
```


## admin connect
```
mongo 
    --host "your master server ip" \
    --port 27017 \
    --tls \
    --tlsCertificateKeyFile ~/.ssl/your key.pem \
    --tlsCAFile ~/.ssl/ca.pem  \
    --authenticationDatabase 'admin' \
    -u "your user name" \
    -p
```







# Use x.509 Certificates instead of password authentication

## Be a root user
Change user name for your fit. Here is a example of user 'moomin'.

### Create user client certification
```
sudo openssl genrsa -out moomin.key 2048
sudo openssl req -new -key moomin.key -out moomin.csr  -subj "/C=JP/ST=Tokyo/L=Tokyo/O=moomin/OU=ITk/CN=192.168.1.32/emailAddress=kim@hep.phys.titech.ac.jp"
```
CN(common-name) should be your bound IP address. e.g. 192.168.1.32


### x509 sign
```
sudo openssl x509 -req -in moomin.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out moomin.crt -days 500 -sha256
sudo cat moomin.key moomin.crt > moomin.pem
```

### Create mongo user
```
openssl x509 -in moomin.pem -inform PEM -subject -nameopt RFC2253
```
The output should be like below:
```
subject= emailAddress=kim@hep.phys.titech.ac.jp,CN=192.168.1.32,OU=ITk,O=moomin,L=Tokyo,ST=Tokyo,C=JP
-----BEGIN CERTIFICATE-----
# ...
-----END CERTIFICATE-----
```

Create a mongo user as emailAddress=kim@hep.phys.titech.ac.jp,CN=192.168.1.32,OU=ITk,O=moomin,L=Tokyo,ST=Tokyo,C=JP
```
mongo \
    --host "your master server ip" \
    --port 27017 \
    --tls \
    --tlsCertificateKeyFile ~/.ssl/your key.pem \
    --tlsCAFile ~/.ssl/ca.pem  \
    --authenticationDatabase 'admin' \
     -u "your user name" \
    -p

use $external
db.createUser(
  {
    user: "emailAddress=kim@hep.phys.titech.ac.jp,CN=192.168.1.32,OU=ITk,O=moomin,L=Tokyo,ST=Tokyo,C=JP",
    roles: [
             { role: 'readWrite', db: 'localdb' } 
           ],
    writeConcern: { w: "majority" , wtimeout: 5000 }
  }
)
```

### Change config file and restart mongoDB server
Add below to config file /etc/mongod.conf
```
security:
    clusterAuthMode: x509
```

then restart
```
systemctl restart mongod.service
```

### Send certificate and key to user
2 files are needed.
```
ca.pem
moomin.pem
```


## Be user
### Log in
```
mongo \
    --host your master host id \
    --tls \
    --tlsCertificateKeyFile ~/.ssl/your key.pem \
    --tlsCAFile ~/.ssl/ca.pem  \
    --authenticationDatabase '$external' \
    --authenticationMechanism MONGODB-X509
```


References.
- [Secure your MongoDB connections - SSL/TLS](https://medium.com/@rajanmaharjan/secure-your-mongodb-connections-ssl-tls-92e2addb3c89)
- [Using Encryption and Authentication to Secure MongoDB](https://www.codeproject.com/Articles/1227164/Using-Encryption-and-Authentication-to-Secure-Mong)
- [Use x.509 Certificates to Authenticate Clients](https://docs.mongodb.com/manual/tutorial/configure-x509-client-authentication/)