## CONTENTS
------------------------
 ## Introduction
 ## prerequisite
 ## How to use
 ## ARCHITECTURAL OVERVIEW
 ## Troubleshooting 

## INTRODUCTION
---------------
Customer: Redis (Michael Ehrig)

The Script.py scrip is created in Python to accomplish the following task by connecting with single sharded Redis Enterprise databases:

* Insert the values 1-100 into the Redis OSS database on source-db. Possible outcomes:
   * The connection is established with source-db endpoint on "redis-13090.re-cluster1.ps-redislabs.org:13090".
	* A list key named as "values" is created to insert 1-100 values. 

* Read and print them in a reverse order from replica-db. Possible outcomes:
	* The connection is established with replica-db endpoint on "redis-12292.re-cluster1.ps-redislabs.org:12292".
	* Retrived the values of key "values" from replica-db and printed them in reverse order (100-1).


## PREREQUISITE
---------------
* 2 Single Sharded Redis Enterprise Databases:
   *  A single sharded Redis Enterprise database named "source-db" with no password, and a memory limit of 2GB. 
   *  Another single sharded Redis Enterprise database named "replica-db" with no password, and a memory limit of 2GB. 
      * Enable "Replica Of" in Advance options and use "source-db" as the source database to make "replica-db" database a repository for keys from "source-db" database.

   Refer the below link to know more about creating Single Sharded Redis Enterprise Databases.
   https://docs.redis.com/latest/rs/administering/creating-databases/

* Python 3.7 and above. Latest version can be dowloaded from https://www.python.org/downloads/.
* Python client for Redis database and key-value store. You can refer the below link to install the latest redis package using PIP:
   * https://pypi.org/project/redis/


## HOW TO USE
-------------
* Install the below required packages using PIP:
   * redis 4.2.2
* Make sure that the your IDE environment is reachable from both the endpoints(Source-db, replica-db).
* Run script.py using the below command:
   * python3 script.py
* script.py script will perform the below action:
   * Calling "insert_values_source_db()" function to perform below actions:
   * Validating the connection with Source-db endpoint.
   * Checking if "values" key already exists or not, if yes then deleting the "values" key to reinitiate the "values" key.
   * Inserting the values 1-100 in "values" key.
   * Calling the "reverse_values_repica_db()" function to retrive the values from "values" key in reverse order.
   * "reverse_values_repica_db()" will validate the connection with replica-db endpoint and also validate if "values" key present in replica-db or not. 
      If not, then check whether replication is working as expected or not.
   * "reverse_values_repica_db()" will print all the values in "values" key in reverse order.


## ARCHITECTURAL OVERVIEW
-------------------------
*Provide a high level overview of the architecture.*

Examples:\
This scripted netscan is written in Groovy and obtains X data using ABC to scan for switches and routers in the customer's environment.

Or:

This script is written in Python and resides on the ABC collector. It is run when XYZ occurs. It communicates DEF to the GHI via JKL data consisting of MNO. 


## TROUBLESHOOTING
------------------
/usr/bin/python3 /home/coder/script.py
*Outline known or common problems that might be encountered along with solutions (links are okay if they point to LogicMonitor Support documents or if the steps are long, but it is helpful to provide a summary since links sometimes go stale).*

Examples:
This DataSource depends on SNMP access. If no data is being returned, please follow [these steps for LogicMonitor SNMP troubleshooting](https://www.logicmonitor.com/support/monitoring/os-virtualization/troubleshooting-snmp).
