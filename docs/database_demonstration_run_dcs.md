# Hook-up the module to the devices and run the DCS controller

## Hook-up module to devices
composing

## Create an ssh tunnel 
In order to connect to influxDB service in the DB machine from your local machine, Run the following comand on your shell.<br>
**Change the server name according to the given name** (e.g.:parrot@localdbserver99)<br> 
Password is the DB server account's password.(Default is "password".)

```bash
$ ssh -L 8086:localhost:8086 parrot@localdbserverXX -fN 
Password:
```
![ssh tunnel influxdb](images/sshtunnel_influxdb.png)

## (a) Run a script to get temperature
To get environmental temperature and store the data into influxDB, do the following command.<br>
<span style="color: red; ">**Don't stop this process during the readout process. Switch the shell from the next step.**</span>

```bash
$ cd ~/work/E4control/e4control
$ python3 temp_controller.py
This measurement runs until ctrl+C is pressed!
Temp1:??.??C     Temp2:??.??C
...
```

## (b) Run LV IV
composing


## (c) Run LV PS controller
To turn on the LV PS and get the current and voltage, do the following command.<br>
<span style="color: red; ">**Don't stop this process during the readout process. Switch the shell from the next step.**</span>
```bash
$ cd ~/work/E4control/e4control
$ python3 LV_controller.py
This measurement runs until ctrl+C is pressed!
TTI2:
...
```
![DCS system](images/demo_dcs_system.png)

## The DCS data monitoring in Grafana
Check the DCS data in "Grafana" by following the link bellow.<br>
[Check DCS data in Grafana](database_demonstration_grafana.md)<br>


Go to next step.<br>
[Retrieve module info and create config files for the scan](database_demonstration_setup_for_scan.md)<br>


