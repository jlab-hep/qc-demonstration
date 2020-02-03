### Q. "No ROOT Software" is displayed in the browser by Viewer Application.

<details><summary>A. PyROOT is required for displaying plots in browser</summary><div>

1. Check if PyROOT is available

   ```bash
   $ for ii in 1 2 3 4; \
   do  if pydoc3 modules | \
   cut -d " " -f ${ii} | \
   grep -x ROOT > /dev/null; \
   then echo "PyROOT is available"; \
   fi; \
   done

   PyROOT is available # Abailable
   "No message"        # Not available
   ``` 

2. Install ROOT software which can use PyROOT by Python3 

   ```bash
   $ root_install_dir=`pwd`
   $ wget https://root.cern.ch/download/root_v6.16.00.source.tar.gz
   $ tar zxf root_v6.16.00.source.tar.gz
   $ rm -f root_v6.16.00.source.tar.gz
   $ mv root-6.16.00 6.16.00
   $ mkdir 6.16.00-build
   $ cd 6.16.00-build
   $ cmake \
   -DCMAKE_INSTALL_PREFIX=${root_install_dir}/6.16.00-install \
   -DPYTHON_EXECUTABLE=/usr/bin/python36 \
   ../6.16.00
   $ cmake --build . -- -j4
   $ make install
   ```

3. Confirm if the installation was successful

   ```bash
   $ source ${root_install_dir}/6.16.00-build/bin/thisroot.sh
   $ for ii in 1 2 3 4; \
   do  if pydoc3 modules | \
   cut -d " " -f${ii} | \
   grep -x ROOT > /dev/null; \
   then echo "PyROOT is available"; \
   fi;  \
   done 

   PyROOT is available
   ```

</div></details>

### Q. How to access the Local DB from another machine (not localhost)

<details><summary>A. Opening firewall port is required for accessing Local DB from another machine</summary><div>

1. Confirm config file

   Add bindIp (default: '127.0.0.1') in MongoDB config file `/etc/mongod.conf`:
 
   ```yaml
   # mongod.conf
   .
   .
   .
   # network interfaces
   net:
     bindIp: 127.0.0.1,"<HOST IP ADDRESS> or <HOSTNAME>"  
     # Listen to local interface only, comment to listen on all interfaces.
     port: 27017
   ```
 
   And start MongoDB service and confirm it works.
 
   ```bash
   $ sudo systemctl restart mongod.service
   ```

2. Open port

   ```bash
   $ sudo firewall-cmd --zone=public --add-port=27017/tcp --permanent
   $ sudo firewall-cmd --reload
   ```

3. Confirm if the setting was successful

   Access `$ mongo --host "HOST IP ADDRESS"` from another machine.

   ```bash
   $ mongo -host "HOST IP ADDRESS"
   MongoDB shell version v3.6.8
   connecting to: mongodb://"HOST IP ADDRESS":27017
   MongoDB server version: 3.6.8
   Server has startup warnings: 
   ```

</div></details>

### Q. How to access the Viewer Application from another machine (not localhost)

<details><summary>A. Apache is required for accessing Viewer from another machine</summary><div>

1. Install libraries

   ```bash
   $ sudo yum install -y httpd.x86_64
   ```

2. Setup http protocol

   ```bash
   $ sudo /usr/sbin/setsebool -P httpd_can_network_connect 1
   $ cp ${db_tools_dir}/scripts/apache/config.conf /etc/httpd/conf.d/localDB-tools.conf
   ```

3. Open port

   ```bash
   $ sudo firewall-cmd --add-service=http --permanent
   $ sudo firewall-cmd --reload
   ```

4. Start service

   ```bash
   $ sudo systemctl start httpd
   $ sudo systemctl enable httpd
   ```

5. Confirm if the setting was successful

   Access "http://<ip address>:5000/" and Local DB Viewer page should be displayed on browser from another machine.

</div></details>

### Q. '#DB ERROR# The connection of Local DB mongodb://127.0.0.1:27017 is BAD.' is displayed.

<details><summary>A. Connection check by `localdbtool-upload init` is failed by some reasons.</summary><div>

1. Uncompleted the setup of Local DB Server

   You can check is as following:
   ```bash
   $ mongo
   # i. MongoDB not installed
   bash: mongo: command not found
   
   # ii. MongoDB not started
   <some texts>
   exception: connect failed
   ```

   1. MongoDB not installed

      You can setup Local DB Server automatically by the script:
      ```bash
      $ git clone https://github.com/jlab-hep/localDB-tools.git
      $ cd localDB-tools/setting
      $ sudo ./db_server_install.sh
      ```
      Check [Setup Local DB Server](#Setup-Local-DB-Server) for more detail.

   2. MongoDB not started

      You can start/restart/enable Mongo DB by systemctl (centOS7):
      ```bash
      $ systemctl restart mongod.service
      $ systemctl enable mongod.service
      ```

2. Mistake Local DB Server Information

   Confirm the database config file and set it properly.
   ```json
   {
       "hostIp": "127.0.0.1",
       "hostPort": "27000",
       "dbName": "localdb",
       "stage": [
           "Bare Module",
           "Wire Bonded",
           "Potted",
           "Final Electrical",
           "Complete",
           "Loaded",
           "Parylene",
           "Initial Electrical",
           "Thermal Cycling",
           "Flex + Bare Module Attachment",
           "Testing"
       ],
       "environment": [
           "vddd_voltage",
           "vddd_current",
           "vdda_voltage",
           "vdda_current",
           "hv_voltage",
           "hv_current",
           "temperature"
       ],
       "component": [
           "Front-end Chip",
           "Front-end Chips Wafer",
           "Hybrid",
           "Module",
           "Sensor Tile",
           "Sensor Wafer"
       ]
   }
   ```
   You might have to change 'hostIp' and 'hostPort' following your Local DB settings.

</div></details>

