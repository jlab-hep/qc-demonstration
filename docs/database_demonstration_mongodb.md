# MongoDB

## Create accounts in mongoDB
Create an account in mongoDB using the following commands.<br>
Input "username" and "password" as you like.(e.g.: USERNAME=hokuyama, PASSWORD=itkweek)<br>
<span style="color: red; ">**These are used as LocalDB admin's username and password.**</span>

```bash
$ cd ~/work/localdb-tools/setting
$ ./create_admin.sh
Authentication succeeded!
Local DB Server IP address: 127.0.0.1
Local DB Server port: 27017
 
Are you sure thats correct? [y/n]
> y

Register localDB admins username: USERNAME
Register localDB admins password: 
Successfully added user:
...
For checking the setting of Local DB: /etc/mongod.conf
```

## Lock mongoDB
Lock the mongoDB so that only those who know the account name and password can read and write to it.<br>
Run the following command.:
```bash
$ sudo echo "security.authorization: enabled" >> /etc/mongod.conf
```
Reload the config file and restart the mongoDB service with the bellow command.
```bash
$ sudo systemctl restart mongod.service
```
Now the mongoDB setup is done! Go to next step.
[Setting for LocalDB viewer](database_demonstration_viewer.md)<br>

