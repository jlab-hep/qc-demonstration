## Installation for the DB machine
For centos7<br>
Setup the DB machine environment.

### Connect to the DB machine via ssh

Please run following command on your shell to connect DB machine via ssh.<br>
We launched a virtual server and tell you the server name.<br>
**Change the server name according to the given name** (e.g.:root@localdbserver1)<br> 
The default password is "password".

```bash
$ ssh parrot@localdbserverXX
Password: 
Last login: ... 2020 from monkeyisland.dyndns.cern.ch
```
![ssh connection](images/ssh_connection.png)

### yum packages
- g++ version 7.0 or higher<br>
```bash
$ sudo yum install -y centos-release-scl
$ sudo yum install -y devtoolset-7
$ source /opt/rh/devtoolset-7/enable
```

- cmake3

```bash
$ sudo yum install -y epel-release
$ sudo yum install -y cmake3
```

- Other dependencies
```bash
$ sudo yum install -y git emacs
```

### Python packages

- python3 version 3.6 or higher

```bash
$ python3 --version
Python 3.6.8
```

- python pip packages
```bash
$ sudo python3 -m pip install arguments coloredlogs Flask Flask-PyMongo Flask-HTTPAuth Flask-Mail pdf2image Pillow prettytable pymongo python-dateutil PyYAML pytz plotly matplotlib numpy requests tzlocal itkdb influxdb pandas
```

### LocalDB tools
Tools to operate LocalDB
```bash
$ cd ~/
$ mkdir work && cd work
$ git clone https://gitlab.cern.ch/YARR/localdb-tools.git
```

### Mongo DB

MongoDB version 4.2 or higher for Local DB<br>
This is the database to store the QC results<br>
**There might be some error masages but please ignore them and proceed.**
```bash
$ cd ~/work/localdb-tools/scripts/shell
$ ./upgrade_mongoDB_centos.sh
[sudo] password for dbuser: XXXXXXX
OK!

----------------------------------------------
[WARNING] MongoDB version 4.2 or greater is required
----------------------------------------------

Install MongoDB version 4.2? [y/n]
y

< Installing packages with many texts >
...
```
Start mongodb

```bash
$ sudo systemctl start mongod.service
```
### influxDB

This is the database to store the DCS data<br>
Run the following the bellow command at once including the last EOF.
```bash
cat <<EOF | sudo tee /etc/yum.repos.d/influxdb.repo
[influxdb]
name = InfluxDB Repository - RHEL \$releasever
baseurl = https://repos.influxdata.com/rhel/\$releasever/\$basearch/stable
enabled = 1
gpgcheck = 1
gpgkey = https://repos.influxdata.com/influxdb.key
EOF
```
Install and start influxDB
```bash
$ sudo yum install -y influxdb
$ sudo systemctl start influxdb
```
### Grafana
This is a web application to see the contents of influxdb.<br>
Run the following command at once.
```bash
cat <<EOF | sudo tee /etc/yum.repos.d/grafana.repo
[grafana]
name=grafana
baseurl=https://packages.grafana.com/oss/rpm
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://packages.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
EOF
```

Install and start grafana
```bash
$ sudo yum install -y grafana
$ sudo systemctl start grafana-server
```

### Root
Root SW installation
```bash
$ sudo yum install -y git cmake gcc-c++ gcc binutils libX11-devel libXpm-devel libXft-devel libXext-devel gcc-gfortran openssl-devel pcre-devel mesa-libGL-devel mesa-libGLU-devel glew-devel ftgl-devel mysql-devel fftw-devel cfitsio-devel graphviz-devel avahi-compat-libdns_sd-devel python-devel libxml2-devel giflib wget
$ cd /opt
$ wget https://root.cern/download/root_v6.18.04.Linux-centos7-x86_64-gcc4.8.tar.gz
$ tar zxf root_v6.18.04.Linux-centos7-x86_64-gcc4.8.tar.gz
$ source /opt/root/bin/thisroot.sh
```
Go to next step.<br>
[Setting for MongoDB](database_demonstration_mongodb.md)<br>

