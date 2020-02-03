Please convert the scheme if you use old version of DB (old-db-v/old-sw-old-db-v/db-v0.8) before using DB SW (v1.0).

___Be sure to back up DB before proceeding with the conversion process.___

```
$ sudo systemctl stop mongod.service
$ date=`date +"%y%m%d"`
$ sudo tar zcvf mongo-${date}.tar.gz /var/lib/mongo
$ sudo systemctl restart mongod.service
```

## 1. Conversion

There are three steps:

- update the structure of "localdb" Database to the latest one
- convert the structure of "yarrdb" Database to the latest one and merge it into "localdb" Database
- verify the structure of "localdb" Database

```
$ git clone https://github.com/jlab-hep/localDB-tools.git
$ cd localDB-tools/scripts/writeDB
$ python3 make_covert.py
# Do you replicate DB: localdb ---> localdb_copy? (y/n) > y
# Continue to convert DB: yarrdb/localdb(old) ---> localdb(latest)? (y/n) > y    
<lot texts> 
```

It takes about 10 minutes for 1GB data size to complete the conversion. <br>
For more detail, check log files made in localDB-tools/scripts/writeDB/log