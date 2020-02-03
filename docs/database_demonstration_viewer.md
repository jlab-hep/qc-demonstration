# Viewer Application

### 1. Setup the Viewer Application by the script 'setup_viewer.sh'
Create config file to setup viewer.<br>
Input localdb admin's username and password in the middle of the command.<br>
(e.g.: USERNAME=hokuyama, PASSWORD=itkweek)

```bash
$ cd ~/work/localdb-tools/viewer
$ ./setup_viewer.sh
Local DB Server IP address: 127.0.0.1
Local DB Server port: 27017
 
[LDB] Are you sure thats correct? [y/n]
> y
 
[LDB] Welcome to Local Database Tools!
...
[LDB] Do you use admin functions for LocalDB viewer? [y/n]
> y
 
Input localDB admins username: USERNAME
Input localDB admins password:  

[LDB] Authentication succeeded![LDB] Check plotting tool...
Cloning into '/root/work/localdb-tools/viewer/plotting-tool'...
...
[LDB] More information: https://localdb-docs.readthedocs.io/en/master/
```

### 2. Start LocalDB viewer with the command 'app.py'
Start LocalDB viewer using the following command.<br>
<span style="color: red; ">**Don't kill this process throughout the course of this tutorial. Use another shell from the next step.**</span>

```bash
$ ./app.py --config admin_conf.yml
Need user authentication.
Authentication succeeded.
2020-01-31 23:25:23 localdbserver.cern.ch matplotlib.font_manager[18847] INFO generated new fontManager
2020-01-31 23:25:23 localdbserver.cern.ch root[18847] INFO [LDB] Viewer Application URL: http://127.0.0.1:5000/localdb/
 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
2020-01-31 23:25:24 localdbserver.cern.ch werkzeug[18847] INFO  * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

Go to next step.<br>
[Installation for DAQ machine](database_demonstration_install_daq_machine.md)<br>
