# Hook-up the module to the devices and run the DCS controller

## Hook-up module to devices
This step has already done.Plrease go to next.

## (a) Run a script to get temperature(for monkeyisland)
To get environmental temperature and store the data into influxDB, do the following command.<br>
<span style="color: red; ">**Don't stop this process during the readout process. Switch the shell from the next step.**</span>
<br>
For monkeyisland,
```bash
$ cd ~/work/E4control/e4control
$ python3 temp_controller.py
This measurement runs until ctrl+C is pressed!
Temp1:??.??C     Temp2:??.??C
...
```
## (b) Run LV IV(for yarrpixdaq)
To run LV IV and get data, do the following command.(only for yarrpixdaq)<br>
```bash
$ cd ~/reference/lowvoltageiv/
$ python makeIVcurve.py
```
You can see the raw data in "IVout_test_0.json".<br>
Create and check the IV plot with the following commands.<br>
```bash
$ python analyzeIV.py -i IVout_test_0 -o test  
$ qpdfview 0x0796_test.png 
```

## (c) Run LV PS controller
To turn on the LV PS and get the current and voltage, do the following command.<br>
<span style="color: red; ">**Don't stop this process during the readout process. Switch the shell from the next step.**</span>
<br>
For monkeyisland,
```bash
$ cd ~/work/E4control/e4control
$ python3 LV_controller.py
This measurement runs until ctrl+C is pressed!
TTI2:
...
```
For yarrpixdaq,
```bash
$ cd ~/reference/lowvoltageiv/
$ python3 LV_controller.py
```


![DCS system](images/demo_dcs_system.png)

## The DCS data monitoring in Grafana
Check the DCS data in "Grafana" by following the link bellow.<br>
[Check DCS data in Grafana](database_demonstration_grafana.md)<br>


Go to next step.<br>
[Retrieve module info and create config files for the scan](database_demonstration_setup_for_scan.md)<br>


