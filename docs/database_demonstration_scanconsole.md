# QC scan

## scanConsole and upload the DCS data

Run the scan using the following command.(e.g. digitalscan)<br>
The scan result is automatically stored when you put "-W" option.
```bash
./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/std_digitalscan.json -W
```
Next, run the dbAccessor to upload the DCS data from influxDB to LocalDB:<br>
For monkeyisland
```bash
./bin/dbAccessor -F localdb/configs/influxdb_connectivity.json -n 20UPGRA0000026 -s data/last_scan/scanLog.json
```
For yarrpixdaq
```bash
./bin/dbAccessor -F localdb/configs/influxdb_connectivity.json -n 20UPGRA0000027 -s data/last_scan/scanLog.json
```
Check the test result and DCS plot from following link [http://127.0.0.1:5000/localdb/scan](http://127.0.0.1:5000/localdb/scan).<br>

![demo scan](images/demo_scan.png)

Test items for tuning are bellow:<br>
- diff_analogscan<br>
- diff_thresholdscan<br>
- diff_totscan<br>
- diff_tune_globalthreshold<br>
- diff_tune_pixelthreshold<br>
- diff_tune_globalpreamp<br>
- diff_retune_pixelthreshold<br>
- diff_tune_finepixelthreshold<br>
- diff_thresholdscan<br>
- diff_totscan<br>

Do this tuning step for the chip using the following commands as a module QC-minick.<br>
If you want to integrate the DCS data for each scan, put the following command between scans.<br>
"./bin/dbAccessor -F localdb/configs/influxdb_connectivity.json -n 20UPGRA0000026 -s data/last_scan/scanLog.json"<br>
or<br>
"./bin/dbAccessor -F localdb/configs/influxdb_connectivity.json -n 20UPGRA0000027 -s data/last_scan/scanLog.json"<br>

```bash
./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_analogscan.json -W
./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_thresholdscan.json -W
./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_totscan.json -t 10000 -W
./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_tune_globalthreshold.json -t 1500 -W
./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_tune_pixelthreshold.json -t 1500 -W
./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_tune_globalpreamp.json -t 10000 -W
./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_retune_pixelthreshold.json -t 1500 -W
./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_tune_finepixelthreshold.json -t 1500 -W
./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_thresholdscan.json -W
./bin/scanConsole -r configs/controller/specCfg.json -c db-data/connectivity.json -s configs/scans/rd53a/diff_totscan.json -t 10000 -W
```
We can also upload the result after the scan.<br>
Add the result path to a cache file(***~/.yarr/localdb/run.dat***). Then, run the following command.
```bash
./localdb/bin/localdbtool-upload cache --database ~/.yarr/localdb/monkeyisland_database.json
```


Check the test results [http://127.0.0.1:5000/localdb/scan](http://127.0.0.1:5000/localdb/scan).<br>
Please use some viewer functions.(download, search, comment, tag...)


We are also developing the script to run these scan at once.<br>
Scan Operator repo ([https://gitlab.cern.ch/YARR/utilities/scan-operator](https://gitlab.cern.ch/YARR/utilities/scan-operator))

Go to next step.<br>
[Select and Upload results into Production DB](database_demonstration_upload_itkpd.md)<br>

