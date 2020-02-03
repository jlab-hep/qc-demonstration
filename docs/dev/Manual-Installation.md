This page describes how to install [libraries](https://github.com/jlab-hep/Yarr/wiki/libraries) and setup machine manually.

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

### 1) MongoDB

Please look at @Install MongoDB Community Edition on Linux](https://docs.mongodb.com/v3.6/administration/install-on-linux/) to install mongoDB server and client.

- version : v3.6

- yum installation for centOS7

  - Add yum repository

    Create `/etc/yum.repos.d/mongodb-org-3.6.repo` as below:

    ```bash
    [mongodb-org-3.6]
    name=MongoDB Repository
    baseurl=https://repo.mongodb.org/yum/redhat/7Server/mongodb-org/3.6/x86_64/
    gpgcheck=1
    enabled=1
    gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
    ```

  - Install by yum

    ```bash
    $ sudo yum install -y mongodb-org.x86_64
    ```

- Start and Confirmation

  Add bindIp (default: '127.0.0.1') in MongoDB config file `/etc/mongod.conf`:

  ```yaml
  # mongod.conf
  .
  .
  .
  # network interfaces
  net:
    bindIp: 127.0.0.1,"HOST IP ADDRESS"  
    # Listen to local interface only, comment to listen on all interfaces.
    port: 27017
  ```

  And start MongoDB service and confirm it works.

  ```bash
  $ sudo systemctl start mongod.service
  $ sudo systemctl enable mongod.service
  $ mongo
  MongoDB shell version v3.6.8
  connecting to: mongodb://localhost:27017
  MongoDB server version: 3.6.8
  Server has startup warnings: 
  ```

### 2) Python

- version : v3.6

  Prepared Local DB tools are based on Python3.

- yum installation for centOS7

  ```bash
  $ sudo yum install -y　\
  epel-release.noarch \
  centos-release-scl.noarch \
  devtoolset-7.x86_64 \
  bc.x86_64 \
  python.x86_64 \
  python36 \
  python36-devel \
  python36-pip \
  python36-tkinter \
  ```

- Confirmation

  ```bash
  $ python36 --version
  Python 3.6.8
  ```

- Module Installation

  Local DB tools need some python modules.

  ```bash
  $ sudo pip3 install \
  arguments \
  coloredlogs \
  Flask \
  Flask-PyMongo \
  Flask-HTTPAuth \
  pdf2image \
  Pillow \
  prettytable \
  pymongo \
  python-dateutil \
  PyYAML \
  pytz \
  madplotlib \
  numpy \
  plotly \
  requests \
  tzlocal
  ```

Next step: [Setup Viewer Application](https://github.com/jlab-hep/Yarr/wiki/Setup-Viewer-Application)

## For DAQ Server

### 1) yum install

- Install by yum

  ```bash
  $ sudo yum install -y　\
  epel-release.noarch \
  centos-release-scl.noarch \
  openssl-devel
  bc.x86_64 \
  wget.x86_64 \
  mongodb-org.x86_64 \
  gnuplot.x86_64 \
  python.x86_64 \
  python36 \
  python36-devel \
  python36-pip \
  python36-tkinter \
  ```

### 2) Python Module install

Local DB tools need some python modules.

  ```bash
  $ sudo pip3 install \
  arguments \
  coloredlogs \
  Flask \
  Flask-PyMongo \
  Flask-HTTPAuth \
  pdf2image \
  Pillow \
  prettytable \
  pymongo \
  python-dateutil \
  PyYAML \
  pytz \
  madplotlib \
  numpy \
  plotly \
  requests \
  tzlocal
  ```

Next step: [Setup DAQ Server](https://github.com/jlab-hep/Yarr/wiki/Setup-DAQ-Server)

-------

Back to the page: [Installation](https://github.com/jlab-hep/Yarr/wiki/Installation)
