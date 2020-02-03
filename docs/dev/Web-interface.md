This page is the instruction to set Viewer Application(https://github.com/jlab-hep/localDB-tools).<br>
You can check data in database via web interface with Viewer Application powered by Python and Flask with PyMongo python module.
> requirements
>* centOS7
>* Local Database is running
>* ROOT software enabled by `source path/to/bin/thisroot.sh`
>* python 2.X or 3.X which can use PyROOT enabled by `source path/to/thispython.sh`

# Installation
## 0) environmental setting
   ```
   source /opt/rh/devtoolset-7/enable
   ```

## 1) Install pip and modules

1) Download localDB-tools
   ```
   git clone https://github.com/jlab-hep/localDB-tools
   cd localDB-tools/viewer
   git checkout devel
   ```

2) Install pip 

   <details><summary>(click)</summary><div>

   * python2
     ```
     $ sudo yum install epel-release
     $ sudo yum install python python-pip poppler-utils
     ```

   * python3
     ```
     sudo yum install epel-release
     sudo yum install python36 python36-devel python36-setuptools
     sudo easy_install-3.6 pip
     ```

   * In case of none-sudo user, do below to install on local.(not recommended)
     ```
     curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
     python get-pip.py --user
     ```

   ---
   </div></details>

3) Install python modules
   ```
   $ cd localDB-tools/scripts/install   
   $ sudo pip install -r requirements.txt
   ```
   > required packages
   >* Click==7.0
   >* Flask==1.0.2
   >* Flask-HTTPAuth>=3.2.4
   >* Flask-PyMongo>=2.1.0
   >* itsdangerous>=1.0.0
   >* Jinja2>=2.10
   >* MarkupSafe>=1.0
   >* pdf2image>=1.0.0
   >* Pillow>=5.3.0
   >* prettytable==0.7.2
   >* pymongo>=3.7.2
   >* python-dateutil>=2.7.5
   >* PyYAML>=3.13
   >* setuptools>=39.2.0
   >* six>=1.11.0
   >* Werkzeug>=0.14.1

## 2) Create configuration file
   ```
   $ cd localDB-tools/viewer
   $ cp ../scripts/yaml/web-conf.yml conf.yml
   ```

# Check

# Usage
   Check [Quick tutorial for Viewer](https://github.com/jlab-hep/Yarr/wiki/Quick-tutorial-for-Viewer)

# Advance
  ## apache
  [more detail](https://github.com/jlab-hep/Yarr/wiki/apache)

-------

Back to the page: [Installation](https://github.com/jlab-hep/Yarr/wiki/Installation)

