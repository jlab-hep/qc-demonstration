There are 2 choices for installation of mongoDB server. We recommend the first one. 

## A. Common way
### 1) Install from common mongoDB repository
Please look at [Install MongoDB Community Edition on Linux](https://docs.mongodb.com/v3.6/administration/install-on-linux/) to install mongoDB server and client.

1) Add yum repository

   Create and open `/etc/yum.repos.d/mongodb-org-3.6.repo`, then insert below and save.
   ```
   [mongodb-org-3.6]
   name=MongoDB Repository
   baseurl=https://repo.mongodb.org/yum/redhat/7Server/mongodb-org/3.6/x86_64/
   gpgcheck=1
   enabled=1
   gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
   ```
   > About mongo DB version
   >> Install **version 3.6 server** because the library is suitable for version 3.6 server.

2) Install
   ```
   $ sudo yum install mongodb-org
   ```

### 2) Start a system server
1) Start
   ```
   $ sudo systemctl start mongod.service
   ```

2) Check
   
   Type `mongo` or `mongo --host localhost --port 27017`. 
   The result will be like below:
   ```
   $ mongo
   MongoDB shell version v3.6.8
   connecting to: mongodb://localhost:27017
   MongoDB server version: 3.6.8
   Server has startup warnings:  
   ```

### Others

* Ensure that MongoDB will start following a system reboot by `sudo systemctl enable mongod.service`

* You can stop a server by typing`sudo systemctl stop mongod.service`

* mongo db server config file is at `/etc/mongod.conf`<br>
The default host is '127.0.0.1' (localhost), and port is '27017'. You can change it by editing the config file then `sudo systemctl restart mongod.service`


## B. Use SCL (not recommended)

### 1) Install from centos-release-scl repository
```
$ sudo yum install rh-mongodb36-mongodb-server rh-mongodb36-mongodb 
```

The binaries will be at `/opt/rh/rh-mongodb36/root/usr/bin`

### 2) Load path
```
$ source /opt/rh/rh-mongodb36/enable 
```

### 3) Start a local server
1) Create a database directory
   ```
   $ cd
   $ mkdir mongodb
   $ cd mongodb
   ```

2) Create a config file for `mongod`

   Create and open a config file named "mongod.conf", then copy below into config
   ```
   # for documentation of all options, see:
   #   http://docs.mongodb.org/manual/reference/configuration-options/
   
   # Where and how to store data.
   storage:
     dbPath: db
     journal:
       enabled: true

   # where to write logging data.
   systemLog:
     destination: file
     logAppend: true
     path: mongod.log 

   # network interfaces
   net:
     port: 27017
     bindIp: 127.0.0.1
   
   # how the process runs
   processManagement:
     timeZoneInfo: /usr/share/zoneinfo
   ```

   > Note
   > > "dbPath: db" in "storage:" means the data directory is 'db'. <br>
       "path: mongod.log" in "systemLog:" means the log will be stored into 'mongod.log'. 

3) Create a storage directory
   ```
   $ mkdir db 
   ```

4) Start a server
   ```
   $ mongod --config mongod.conf & 
   ```

* Stop a server
  First type `mongo` to use mongo shell, then 
  ```
  use admin
  db.shutdownServer()
  ```

  (To kill local user server, Find job number by typing `ps aux | grep mongod`. Then `kill 5711`)

## If there is problem
* If SELinux is in enforcing mode, 

  enable access to the relevant ports that the MongoDB deployment will use (e.g. 27017). <br>
  For default settings, this can be accomplished by running: <br>
  ```
  $  semanage port -a -t mongod_port_t -p tcp 27017 
  ```
