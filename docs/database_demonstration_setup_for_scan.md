#Setup and create config files for the scan
## Create ssh tunnel 
In order to connect to the mongoDB in the DB machine from your local machine, Run the following comand on your shell.<br>
**Change the server name according to the given name** (e.g.:parrot@localdbserver99)<br> 
Password is the DB server account's password.(Default is "password".)

```bash
$ ssh -L 27017:localhost:27017 parrot@localdbserverXX -fN -p22
Password:
```
![ssh tunnel mongodb](images/sshtunnel_mongodb.png)

## (a). Set username and password for mongodb 
Set username and password using the command bellow to connect to the mongoDB with authentication.<br>
Input LocalDB admin's username and password that you have set prebiously.
```bash
$ cd ~/work/Yarr
$ source localdb/login_mongodb.sh
Input mongodb accounts username: 
Input mongodb accounts password: 
[LDB]Username and password are saved.
```

## (b). Setup database config
Set the config files using the following command to save the mongoDB's information.<br>
You don't have to change anything in this tutorial. Please answer "y" in all steps.
```bash
$ ./localdb/setup_db.sh
[LDB] Set editor command ...
[LDB] > emacs
[LDB]
[LDB] Checking Python Packages ...
[LDB]     ... OK!
[LDB]
[LDB] Checking Database Config: ...
[LDB]
[LDB] -----------------------
[LDB] --  Mongo DB Server  --
[LDB] -----------------------
[LDB] IP address       : 127.0.0.1
[LDB] port             : 27017
[LDB] database name    : localdb
[LDB] -----------------------
[LDB]
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
...
[LDB] -----------------------
[LDB] --  User Information --
[LDB] -----------------------
[LDB] User Name        : 
[LDB] User Institution : 
[LDB] -----------------------
[LDB]
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
...
[LDB] -----------------------
[LDB] --  Site Information --
[LDB] -----------------------
[LDB] site name        : 
[LDB] -----------------------
[LDB]
[LDB] Are you sure that is correct? (Move to edit mode when answer 'n') [y/n/exit]
[LDB] > y
...
[LDB]   Access 'https://localdb-docs.readthedocs.io/en/master/'
```

## (c). Create scan config files from mongodb
To create config files for scanConsole of YARR-SW, Run the command bellow.<br>
(We use the downloaded component's peoperty. Device's serial number is "20UPGRS0000009", chip's serial number is "20UPGRA0000026")
```bash
$ ./localdb/bin/localdbtool-retrieve pull --chip 20UPGRS0000009 
#DB WARNING# Not found test data of the component: 20UPGRS0000009
#DB INFO# component data ID: 5e30318ca13f8d000aa2a22b 
#DB INFO# - Parent    : 20UPGRS0000009 (module)
#DB INFO# - Chip Type : RD53A
#DB INFO# - Chips     : 20UPGRA0000026
#DB INFO# Retrieve ... ./db-data/20UPGRA0000026.json
#DB INFO# Retrieve ... ./db-data/connectivity.json
#DB INFO# -----------------------
```
The config files for the module are generated in 'db-data'.<br>

## (d). Change stage name in the scan config file
Edit the connectivity file(***db-data/connectivity.json***) and change stage name to "WIREBONDING".
```json
{
    "stage": "WIREBONDING",
    "chips": [
        {
            "config": "./db-data/20UPGRA0000026.json",
            "tx": 0,
            "rx": 0
        }
    ],
    "module": {
        "serialNumber": "20UPGRS0000009",
        "componentType": "module"
    },
    "chipType": "RD53A"
}
```

## (e). Change the DCS uploader config file
To include DCS data to the scan result, edit the DCS uploader config file (***localdb/configs/influxdb_connectivity.json***) as follows:
```json
{
    "environments" : [
        {
            "measurement" : "Temperature",
            "dcsList" : [
                {
                    "key"        : "temperature",
                    "data_name"  : "temp1",
                    "data_unit"  : "temp1_unit",
                    "description": "Room Temperature [C]",
                    "setting"    : 28
                },{
                    "key"        : "temperature",
                    "data_name"  : "temp2",
                    "data_unit"  : "temp2_unit",
                    "description": "Board Temperature [C]",
                    "setting"    : 28
                }
            ]
        },{
            "measurement" : "LV",
            "dcsList" : [
                {
                    "key"        : "vddd_voltage",
                    "data_name"  : "LV_Voltage",
                    "data_unit"  : "LV_Voltage_unit",
                    "description": "VDDD Voltage [V]",
                    "setting"    : 1.75
                },
                {
                    "key"        : "vddd_current",
                    "data_name"  : "LV_Current",
                    "data_unit"  : "LV_Current_unit",
                    "description": "VDDD Current [A]",
                    "setting"    : 1.1
                }
            ]
        }
    ]
}
```
Go to next step.<br>
[QC scan](database_demonstration_scanconsole.md)<br>

