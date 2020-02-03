# Advance for mongoDB server
Be careful and think again what you are doing before go on.

To open a server, we recommend to install mongo DB server from official rpm repository.

After install a mongo DB server.

## Contents
* `/etc/mongod.conf` : config file of mongodb

  ```
  systemLog:
    destination: file
    logAppend: true
    path: /var/log/mongod/mongod.log  # where to write logging data
  
  storage:
    dbPath: /var/lib/mongo  # where to store data
    journal:
      enabled: true
  net:
    bindIp: 127.0.0.1, XXX.X.X.X # the hostnames a/o IP addresses a/o full Unix domain socket paths on which mongos and mongod should listen for client connections
    port: 27017 # The TCP port on which the MongoDB instance listens for client connections
  ```

* `/var/log/mongod/mongod.log` : where to write logging data

* `/var/lib/mongo` : where to store data

## Start mongod
```
systemctl enable mongod
systemctl start mongod
```

## Use mongo data directory from other site

1) stop mongod
   ```
    $ sudo systemctl stop mongod.service 
   ```

2) Backup (or delete) original mongo directory
   ```
    $ sudo tar zcvf /var/lib/mongo_backup.tar.gz /var/lib/mongo 
   ```

3) Download and copy data directory
   ```
    $ tar zxvf mongo-181109-fixed.tar.gz
    $ sudo mv var/lib/mongo /var/lib/. 
   ```

4) Change permission, context
   ```
    $ sudo chcon -R -u system_u -t mongod_var_lib_t /var/lib/mongo/  
    $ sudo chown -R mongod:mongod /var/lib/mongo 
   ```

5) Restart mongo
   ```
    $ sudo systemctl start mongod.service
   ```

## Backup mongoDB database
```
 $ sudo systemctl stop mongod.service
 $ date=`date +"%y%m%d"`
 $ sudo tar zcvf mongo-${date}.tar.gz /var/lib/mongo
 $ sudo systemctl restart mongod.service
```

## Contarol users for mongoDB server
### Create admin user
Connect to mongoDB server and create admin server.
```
user
db.createUser({
  user:"admin",
  pwd:"password",
  roles:[{ role:"userAdminAnyDatabase", db:"admin" }]
})
```
(or set roles as roles:["root"] for super user)

### Create user
Create user for YARR software.
```
use yarrdb
db.createUser({
    user: "yarr",
    pwd:"yarrpass",
    roles:[{role:"readWrite",  db:"yarrdb"}]
})
```

Also, create user for web viewer.
```
use yarrdb
db.createUser({
      user: "viewer",
      pwd: "viewerpass",
      roles: [{role: "read", db: "yarrdb"}]
})
```

### Apply the changes and restart the server
Edit config file(/etc/mongod.conf) and add below:
```
security:
  authorization: enabled
```
Then, restart the server `systemctl restart mongod`


### Authenticate
For example to use admin:
```
use admin
db.auth("admin","password")
```

For example to use yarrdb:
```
use yarrdb
db.auth("yarr","yarrpass")
```


## Open port
Do not open port to network unless you are network expert!
```
firewall-cmd --zone=public --add-port=27017/tcp --permanent
firewall-cmd --reload
``` 
