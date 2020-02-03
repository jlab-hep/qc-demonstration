This page describes how to install [libraries](https://github.com/jlab-hep/Yarr/wiki/libraries) and setup machine automatically using the installation.

Contents
---
* [Pre Requirements](#Pre-Requirements)
* [Libraries Installation](#Libraries-Installation)
  * [For DB Server](#For-DB-Server)
  * [For DAQ Server](#For-DAQ-Server)

# Pre Requirements
  * centOS7
  * sudo user account (for installation)
  * git 

    ```bash
    $ sudo yum install git
    ```

# Libraries Installation

## For DB Server

* Installer: `localDB-tools/setting/db_server_install.sh` 

  <span style="color:red">__requirement: sudo user account__</span>

  <span style="color:red">__This installer should be run once for setting the machine.__</span><br>
  <span style="color:red">__After the second run, the missing one will be installed with avoiding duplicate installation.__</span><br>
  <span style="color:red">__But Local DB will be initialized.__</span>

  * Install libraries
  * Open firewall port (http, 27017/tcp)
  * Start Apache service
  * Initialize Local DB
  * Start MongoDB service

  ```bash
  $ git clone https://github.com/jlab-hep/localDB-tools.git
  $ git checkout devel
  $ cd localDB-tools/setting
  $ ./db_server_install.sh
  [LDB] This script performs ...

  [LDB]  - Install yum packages: '~/localDB-tools/setting/requirements-yum.txt'
  [LDB]         $ sudo yum install $(cat ~/localDB-tools/setting/requirements-yum.txt)
  [LDB]  - Install pip modules: '~/localDB-tools/setting/requirements-pip.txt'
  [LDB]         $ sudo pip3 install $(cat ~/localDB-tools/setting/requirements-pip.txt)
  [LDB]  - Start Apache Service:
  [LDB]         $ sudo /usr/sbin/setsebool -P httpd_can_network_connect 1
  [LDB]         $ sudo firewall-cmd --add-service=http --permanent
  [LDB]         $ sudo firewall-cmd --reload
  [LDB]         $ sudo systemctl start httpd
  [LDB]  - Initialize Local DB Server:
  [LDB]         IP address: XXX.XXX.XX.XX
  [LDB]         port      : 27017
  [LDB]         Backup data in Local DB ('/var/lib/mongo') into '/var/lib/mongo-190726.tar.gz'
  [LDB]         Reset data in Local DB
  [LDB]  - Start MongoDB Service:
  [LDB]         $ sudo firewall-cmd --zone=public --add-port=27017/tcp --permanent
  [LDB]         $ sudo firewall-cmd --reload 
  [LDB]         $ sudo systemctl start mongod
  [LDB]         $ sudo systemctl enable mongod

  [LDB] Continue? [y/n]
  > y
  # answer here after confirmation

  [sudo] password:
  [LDB] OK!
  <lots of texts>
  [2019-07-26 07:05:37]  [LDB] Done.
  ```
  Logfile: `localDB-tools/setting/instlog/${datetime}`
  README: `localDB-tools/setting/README

Next step: [Setup Viewer Application](https://github.com/jlab-hep/Yarr/wiki/Setup-Viewer-Application)

## For DAQ Server

* Installer: `YARR/localdb/db_yarr_install.sh`

  <span style="color:red">__requirement: sudo user account__</span>

  <span style="color:red">__This installer should be run once for setting the machine.__</span><br>
  <span style="color:red">__After the second run, the missing one is installed with avoiding duplicate installation.__</span>

  * install libraries

  ```bash
  $ git clone https://gitlab.cern.ch/YARR/YARR.git
  $ cd YARR
  $ git checkout devel
  $ cd localdb
  $ ./db_yarr_install.sh
  [LDB] This script performs ...

  [LDB]  - Install yum packages: '~/YARR/localdb/setting/requirements-yum.txt'
  [LDB]         $ sudo yum install $(cat ~/YARR/localdb/setting/requirements-yum.txt)
  [LDB]  - Install pip modules: '~/YARR/localdb/setting/requirements-pip.txt'
  [LDB]         $ sudo pip3 install $(cat ~/YARR/localdb/setting/requirements-pip.txt)
  [LDB] Continue? [y/n]
  > y

  [sudo] password:
  [LDB] OK!
  ```
  Logfile: `YARR/localdb/setting/instlog/${datetime}`
  README: `YARR/localdb/setting/README

Next step: [Setup DAQ Server](https://github.com/jlab-hep/Yarr/wiki/Setup-DAQ-Server)

-------

Back to the page: [Installation](https://github.com/jlab-hep/Yarr/wiki/Installation)
