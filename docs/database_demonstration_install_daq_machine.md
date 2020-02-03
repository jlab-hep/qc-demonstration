## Installation of the DAQ machine
For centos7<br>
Setup the DAQ machine environment in this page. <br>
<span style="color: red; ">**Use another shell than the DB machine's one and check if you are in local.**</span>

### Yarr SW
Install "Yarr" in "work" directry:

```bash
$ cd ~/work
```
Please follow the link bellow to install Yarr-SW.<br>
[Yarr installation](https://yarr.readthedocs.io/en/latest/install/)


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
[Download module ID infos](database_demonstration_download_itkpd.md)<br>
