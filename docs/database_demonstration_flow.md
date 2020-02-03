# QC Demonstration

## Structure of SW and DB
![SW_Structure](images/SW_Structure.png)
Production DB: A central DB for ITk,setup in Czech.<br>
MongoDB: A local DB to store module info, scan results and so on.<br>
InfluxDB: A DB dedicated for time series data to store DCS data. <br>
LocalDB viewer: A web application to see the contents of mongoDB.<br>
Grafana: A web application to see the contents of influxDB.<br><br>

In this tutorial, we suppose we have two machines, a DAQ machine and a DB machine.<br>
The DAQ machine is the local machine you use in the room. <br>
Run YARR-SW and DCS controller. Get scan results and DCS data in this machine and send the obtained data to the DB machine.<br>
The DB machine is a virtual remote machine which store the scan and DCS data.<br>
MongoDB, InfluxDB and some related services are provided.<br><br>
First, we create the environment for the QC tutorial to install the DB and SW for both machines. Then we demonstrate QC procedure according to the tutorial bellow.<br>

## Tutorial
In this QC demonstration, we can learn the following things:

**The beggining processes**
### 1. Installation for the DB machine
[Installation for the DB machine](database_demonstration_install_db_machine.md)<br>
[Setting for MongoDB](database_demonstration_mongodb.md)<br>
[Setting for LocalDB viewer](database_demonstration_viewer.md)<br>

### 2. Installation for the DAQ machine
[Installation for the DAQ machine](database_demonstration_install_daq_machine.md)<br>

### 3. Download module ID info from the Production DB
[Download Module ID info](database_demonstration_download_itkpd.md)<br><br><br>

**The processes per module per stage.**
### 4. Setup for the QC scan 
[Hook-up the module to the devices and Run the DCS controller](database_demonstration_run_dcs.md)<br>
[Retrieve module info and create config files for the scan](database_demonstration_setup_for_scan.md)<br>

### 5. What to do to run the QC
[What to do for QC scan](database_demonstration_scanconsole.md)<br>

### 6. Upload scan results to the Production DB 
[Select and Upload results to the Production DB](database_demonstration_upload_itkpd.md)<br>

## Appendix
1. Document of "Traveling module"[(https://moduledaqdb.readthedocs.io/en/latest/)](https://moduledaqdb.readthedocs.io/en/latest/)
2. Yarr docs[(https://yarr.readthedocs.io/en/latest/)](https://yarr.readthedocs.io/en/latest/)
3. LocalDB docs[(https://localdb-docs.readthedocs.io/en/master/)](https://localdb-docs.readthedocs.io/en/master/)
4. Tutorial page for ITk production DB[(https://gitlab.cern.ch/jpearkes/itkpd_tutorial/blob/master/README.md)](https://gitlab.cern.ch/jpearkes/itkpd_tutorial/blob/master/README.md)
5. Module QC documentation[(https://cds.cern.ch/record/2702738/files/ATL-COM-ITK-2019-045.pdf?)](https://cds.cern.ch/record/2702738/files/ATL-COM-ITK-2019-045.pdf?)
6. MongoDB web[(https://www.mongodb.com)](https://www.mongodb.com)
7. InfluxDB web[(https://www.influxdata.com)](https://www.influxdata.com)
8. Gragfana web[(https://grafana.com)](https://grafana.com)

## Contact
Let me know if you have questions or comments.<br>
E-mail:hiroki.okuyama at cern.ch<br>
Mattermost:[https://mattermost.web.cern.ch/yarr/channels/localdb](https://mattermost.web.cern.ch/yarr/channels/localdb)
<!--
![demo flow](images/demo_flow.png)
-->
