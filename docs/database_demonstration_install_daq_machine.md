## Installation of the DAQ machine
For centos7<br>
Setup the DAQ machine environment in this page. <br>

<span style="color: red; ">**These SW and packages have already installed in the DAQ . Skip this step.**</span>

### Yarr SW
Install "Yarr" in "work" directry:

```bash
$ cd ~/work
```
Please follow the link bellow to install Yarr-SW.<br>
[Yarr installation](http://yarr.web.cern.ch/yarr/install/)


### Python packages
- python3 version 3.6 or higher
```bash
$ python3 --version
Python 3.6.8
```
- python pip packages
```bash
$ sudo python3 -m pip install arguments coloredlogs pdf2image Pillow pymongo python-dateutil PyYAML pytz matplotlib numpy requests tzlocal influxdb pandas
```

Go to next step.<br>
[Create ssh tunnels from the DAQ machine to the DB machine](database_demonstration_create_ssh_tunnel.md)<br>
