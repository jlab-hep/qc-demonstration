This page describes about libraries required for Local DB

### OS supported by the Wiki
* centOS7

## For DAQ Server
  * [YARR](https://gitlab.cern.ch/YARR/YARR)
  
  * Libraries (MongoDB (v3.6.3), OpenSSL)
    <details><summary>yum packages</summary><div>
    
    ```
    $ sudo yum install \
    epel-release.noarch \
    centos-release-scl.noarch \
    bc.x86_64 \
    mongodb-org.x86_64 \
    devtoolset-7.x86_64 \
    gnuplot.x86_64 \
    openssl-devel \
    python.x86_64 \
    python36 \
    python36-devel \
    python36-pip \
    python36-tkinter 
    ```

    </div></details>

    <details><summary>pip modules</summary><div>

    ```
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
    matplotlib \
    numpy \
    plotly \
    requests \
    tzlocal 
    ```

    </div></details>

## For DB Server
  * [Local DB Tools](https://github.com/jlab-hep/localDB-tools.git)
  * Libraries (MongoDB (v3.6.3), Python3)
    <details><summary>yum packages</summary><div>
    
    ```
    $ sudo yum install \
    epel-release.noarch \
    centos-release-scl.noarch \
    bc.x86_64 \
    mongodb-org.x86_64 \
    devtoolset-7.x86_64 \
    gnuplot.x86_64 \
    python.x86_64 \
    httpd.x86_64 \
    python36 \
    python36-devel \
    python36-pip \
    python36-tkinter 
    ```

    </div></details>

    <details><summary>pip modules</summary><div>

    ```
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
    plotly \
    matplotlib \
    numpy \
    requests \
    tzlocal
    ```

    </div></details>

  * PyROOT for making plots by the Viewer
