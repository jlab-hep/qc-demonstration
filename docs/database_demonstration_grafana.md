# grafana

### Create an ssh tunnel 
In order to see grafana on your browser, Run the following comand on your shell.<br>
**Change the server name accordingly** (e.g.:root@localdbserver99)<br> 
Password is the DB server account's password.(Default is "password".)

```bash
$ ssh -L 3000:localhost:3000 root@localdbserverXX -fN
Password:
```
![ssh tunnel grafana](images/sshtunnel_grafana.png)

### (a) Access to the Web Page

Access to [http://127.0.0.1:3000/](http://127.0.0.1:3000/) with the machine's browser on the same network as DB machine,<br>
and you can see the web page as follows:


### (b) Login

Login with the username: 'admin' and the password: 'admin'
![grafana top](images/demo_grafana_top.png)

### (c) Add Database Source

1. Click "Add data source"
2. Click "InfluxDB"

![grafana add db source](images/demo_grafana_db_source_1.png)<br>
![grafana add db source](images/demo_grafana_db_source_2.png)

3. Set URL "http://localhost:8086"
4. Set Database "dcsDB"
5. Click "Save & Test"

![grafana add db source](images/demo_grafana_db_source_3.png)

### (d) Create New Dashboard

1. Click "+"
2. Click "Add Query"

![grafana add dashboard](images/demo_grafana_db_source_4.png)

3. Select the measurement channel (e.g. "Tempareture")
4. Select data value from the list (e.g. temp1)

![grafana add dashboard](images/demo_grafana_db_source_5.png)

Go to next step.<br>
[scanConsole and tuning](database_demonstration_scanconsole.md)<br>
