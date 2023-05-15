1) Pull the image
-----------------

docker pull d0tfl0w/oracledb:21.3.0.0


2) Create the container
-----------------------

docker run -d --name oracle-db -v OracleDBData:/opt/oracle/oradata -p 1521:1541 -e ORACLE_SID=prodcdb -e ORACLE_PDB=prod -e ORACLE_PWD=Ma7ager#123 -e ORACLE_EDITION=enterprise -e ORACLE_CHARACTERSET=AL32UTF8 -e ENABLE_ARCHIVELOG=true d0tfl0w/oracledb:21.3.0.0

Parameters:
 --name:                 The name of the container. (Default: auto-generated
 -p:                     The port mapping of the host port to the container port.
                         Two ports are exposed: 1521 (Oracle Listener), 5500 (OEM Express)
 -e ORACLE_SID:          The Oracle Database SID that should be used.(Default:ORCLCDB)
 -e ORACLE_PDB:          The Oracle Database PDB name that should be used. (Default: ORCLPDB1)
 -e ORACLE_PWD:          The Oracle Database SYS, SYSTEM and PDBADMIN password. (Default: auto-generated)
 -e INIT_SGA_SIZE:       The total memory in MB that should be used for all SGA components (Optional)
 -e INIT_PGA_SIZE:       The target aggregate PGA memory in MB that should be used for all server processes attached to the instance (Optional)
 -e ORACLE_EDITION:      The Oracle Database Edition [enterprise|standard]. (Default: enterprise)
 -e ORACLE_CHARACTERSET: The character set that you want used when creating the database. (Default: AL32UTF8)
 -e ENABLE_ARCHIVELOG    The ARCHIVELOG mode. By default, set to false. 
                         If set to true, then ARCHIVLOG mode is enabled in the database (for fresh database creation only)
 -v /opt/oracle/oradata
                         The data volume that you want used for the database. Must be writable by the oracle user (uid: 54321) inside the container
                         If omitted, then the database will not be persisted over container recreation.
 -v /opt/oracle/scripts/startup | /docker-entrypoint-initdb.d/startup
                         Optional: A volume with custom scripts to be run after database startup.
                         For further details see the section "Running scripts after setup and on
                         startup" section below.
 -v /opt/oracle/scripts/setup | /docker-entrypoint-initdb.d/setup
                         Optional: A volume with custom scripts that you want run after database setup.
                         For further details see the "Running scripts after setup and on startup" section below.


3) See the status of database
-----------------------------

docker logs oracle-db


ubantu@oracledb:~$ docker logs oracle-db
[2023:05:15 09:03:31]: Acquiring lock .PRODCDB.create_lck with heartbeat 30 secs
[2023:05:15 09:03:31]: Lock acquired
[2023:05:15 09:03:31]: Starting heartbeat
[2023:05:15 09:03:31]: Lock held .PRODCDB.create_lck
ORACLE EDITION: ENTERPRISE

LSNRCTL for Linux: Version 21.0.0.0.0 - Production on 15-MAY-2023 09:03:32

Copyright (c) 1991, 2021, Oracle.  All rights reserved.

Starting /opt/oracle/product/21c/dbhome_1/bin/tnslsnr: please wait...

TNSLSNR for Linux: Version 21.0.0.0.0 - Production
System parameter file is /opt/oracle/homes/OraDB21Home1/network/admin/listener.ora
Log messages written to /opt/oracle/diag/tnslsnr/f816777bf1e4/listener/alert/log.xml
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))

Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=IPC)(KEY=EXTPROC1)))
STATUS of the LISTENER
------------------------
Alias                     LISTENER
Version                   TNSLSNR for Linux: Version 21.0.0.0.0 - Production
Start Date                15-MAY-2023 09:03:32
Uptime                    0 days 0 hr. 0 min. 0 sec
Trace Level               off
Security                  ON: Local OS Authentication
SNMP                      OFF
Listener Parameter File   /opt/oracle/homes/OraDB21Home1/network/admin/listener.ora
Listener Log File         /opt/oracle/diag/tnslsnr/f816777bf1e4/listener/alert/log.xml
Listening Endpoints Summary...
  (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))
The listener supports no services
The command completed successfully
Prepare for db operation
8% complete
Copying database files
31% complete
Creating and starting Oracle instance
32% complete
36% complete
40% complete
43% complete
46% complete
Completing Database Creation
51% complete
54% complete
Creating Pluggable Databases
ubantu@oracledb:~$


---


ubantu@oracledb:~$ docker logs oracle-db
[2023:05:15 09:03:31]: Acquiring lock .PRODCDB.create_lck with heartbeat 30 secs
[2023:05:15 09:03:31]: Lock acquired
[2023:05:15 09:03:31]: Starting heartbeat
[2023:05:15 09:03:31]: Lock held .PRODCDB.create_lck
ORACLE EDITION: ENTERPRISE

LSNRCTL for Linux: Version 21.0.0.0.0 - Production on 15-MAY-2023 09:03:32

Copyright (c) 1991, 2021, Oracle.  All rights reserved.

Starting /opt/oracle/product/21c/dbhome_1/bin/tnslsnr: please wait...

TNSLSNR for Linux: Version 21.0.0.0.0 - Production
System parameter file is /opt/oracle/homes/OraDB21Home1/network/admin/listener.ora
Log messages written to /opt/oracle/diag/tnslsnr/f816777bf1e4/listener/alert/log.xml
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))

Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=IPC)(KEY=EXTPROC1)))
STATUS of the LISTENER
------------------------
Alias                     LISTENER
Version                   TNSLSNR for Linux: Version 21.0.0.0.0 - Production
Start Date                15-MAY-2023 09:03:32
Uptime                    0 days 0 hr. 0 min. 0 sec
Trace Level               off
Security                  ON: Local OS Authentication
SNMP                      OFF
Listener Parameter File   /opt/oracle/homes/OraDB21Home1/network/admin/listener.ora
Listener Log File         /opt/oracle/diag/tnslsnr/f816777bf1e4/listener/alert/log.xml
Listening Endpoints Summary...
  (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))
The listener supports no services
The command completed successfully
Prepare for db operation
8% complete
Copying database files
31% complete
Creating and starting Oracle instance
32% complete
36% complete
40% complete
43% complete
46% complete
Completing Database Creation
51% complete
54% complete
Creating Pluggable Databases
58% complete
77% complete
Executing Post Configuration Actions
100% complete
Database creation complete. For details check the logfiles at:
 /opt/oracle/cfgtoollogs/dbca/PRODCDB.
Database Information:
Global Database Name:PRODCDB
System Identifier(SID):PRODCDB
Look at the log file "/opt/oracle/cfgtoollogs/dbca/PRODCDB/PRODCDB.log" for further details.

SQL*Plus: Release 21.0.0.0.0 - Production on Mon May 15 09:13:18 2023
Version 21.3.0.0.0

Copyright (c) 1982, 2021, Oracle.  All rights reserved.


Connected to:
Oracle Database 21c Enterprise Edition Release 21.0.0.0.0 - Production
Version 21.3.0.0.0

SQL>
System altered.

SQL>
System altered.

SQL>
Pluggable database altered.

SQL>
PL/SQL procedure successfully completed.

SQL> SQL>
Session altered.

SQL>
User created.

SQL>
Grant succeeded.

SQL>
Grant succeeded.

SQL>
Grant succeeded.

SQL>
User altered.

SQL> SQL> Disconnected from Oracle Database 21c Enterprise Edition Release 21.0.0.0.0 - Production
Version 21.3.0.0.0
The Oracle base remains unchanged with value /opt/oracle

Executing user defined scripts
/opt/oracle/runUserScripts.sh: running /opt/oracle/scripts/extensions/setup/swapLocks.sh
[2023:05:15 09:13:19]: Releasing lock .PRODCDB.create_lck
[2023:05:15 09:13:19]: Lock released .PRODCDB.create_lck
[2023:05:15 09:13:19]: Acquiring lock .PRODCDB.exist_lck with heartbeat 30 secs
[2023:05:15 09:13:19]: Lock acquired
[2023:05:15 09:13:19]: Starting heartbeat
[2023:05:15 09:13:19]: Lock held .PRODCDB.exist_lck

DONE: Executing user defined scripts

The Oracle base remains unchanged with value /opt/oracle
#########################
DATABASE IS READY TO USE!
#########################
The following output is now a tail of the alert.log:
PROD(3):ALTER DATABASE DEFAULT TABLESPACE "USERS"
PROD(3):Completed: ALTER DATABASE DEFAULT TABLESPACE "USERS"
2023-05-15T09:13:18.064177+00:00
ARC1 (PID:2830): Archived Log entry 1 added for B-1136883934.T-1.S-2 ID 0x7f61badb3e5d LAD:1 [krse.c:4933]
2023-05-15T09:13:18.455972+00:00
ALTER SYSTEM SET control_files='/opt/oracle/oradata/PRODCDB/control01.ctl' SCOPE=SPFILE;
2023-05-15T09:13:18.475861+00:00
ALTER SYSTEM SET local_listener='' SCOPE=BOTH;
ALTER PLUGGABLE DATABASE PROD SAVE STATE
Completed: ALTER PLUGGABLE DATABASE PROD SAVE STATE
ubantu@oracledb:~$



4) Connect to the oracle database
---------------------------------

$ docker exec -it oracle-db  sqlplus / as sysdba
$ docker exec -it oracle-db  sqlplus sys/cdb-user-password@cdb-sid as sysdba
$ docker exec -it oracle-db  sqlplus system/cdb-user-password@cdb-sid
$ docker exec -it oracle-db  sqlplus pdbadmin/pdb-user-password@pdbname


5) Connect from container and connect to the database

docker exec -it oracle-db /bin/bash  

bash-4.2$ export ORACLE_SID=PRODCDB
bash-4.2$ export ORACLE_HOME=/opt/oracle/product/21c/dbhome_1
bash-4.2$ export PATH=$ORACLE_HOME/bin:$PATH
bash-4.2$
bash-4.2$ sqlplus '/as sysdba'

SQL*Plus: Release 21.0.0.0.0 - Production on Mon May 15 09:22:59 2023
Version 21.3.0.0.0

Copyright (c) 1982, 2021, Oracle.  All rights reserved.


Connected to:
Oracle Database 21c Enterprise Edition Release 21.0.0.0.0 - Production
Version 21.3.0.0.0

SQL> select name, open_mode from v$database;

NAME      OPEN_MODE
--------- --------------------
PRODCDB   READ WRITE

SQL> show pdbs

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 PROD                           READ WRITE NO
SQL>

 

