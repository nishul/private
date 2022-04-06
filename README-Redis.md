## CONTENTS
------------------------
 * Introduction
 * prerequisite
 * How to use
 * Troubleshooting 

## INTRODUCTION
---------------
Customer: Redis (Michael Ehrig)

There are 2 Single Sharded Redis Enterprise Databases(source-db & replica-db) and replica-db is configured as replica of source-db. 
There are 3 Redis Enterprise nodes with a cluster already configured between them: re-n1, re-n2, re-n3. Load node is also configured to load data on "source-db" database using to "memtier_benchmark". 
The "/tmp/memtier_benchmark.txt" file is created in Load node that contains commands used to load the data in "source-db".


The Script.py script is created in Python to accomplish the following task by connecting with single sharded Redis Enterprise databases:

* Insert the values 1-100 into the Redis OSS database on source-db. Possible outcomes:
   * The connection is established with source-db endpoint on "redis-13090.re-cluster1.ps-redislabs.org:13090".
	* A list key named as "values" is created to insert 1-100 values. 

* Read and print them in a reverse order from replica-db. Possible outcomes:
	* The connection is established with replica-db endpoint on "redis-12292.re-cluster1.ps-redislabs.org:12292".
	* Retrived the values of key "values" from replica-db and printed them in reverse order (100-1).


## PREREQUISITE
---------------
* 2 Single Sharded Redis Enterprise Databases:
   *  A single sharded Redis Enterprise database named "source-db" with password as "nopassword", and a memory limit of 2GB. 
   *  Another single sharded Redis Enterprise database named "replica-db" with password as "nopassword", and a memory limit of 2GB. 
      * Enable "Replica Of" in Advance options and use "source-db" as the source database to make "replica-db" database a repository for keys from "source-db" database.

   Refer the below link to know more about creating Single Sharded Redis Enterprise Databases.
   https://docs.redis.com/latest/rs/administering/creating-databases/

* Python 3.7 and above. Latest version can be dowloaded from the below link:
  https://www.python.org/downloads/
* Python client for Redis database and key-value store. You can refer the below link to install the latest redis package using PIP:
  https://pypi.org/project/redis/


## HOW TO USE
-------------
* Install the below required packages using PIP:
   * redis 4.2.2
* Make sure that the your IDE environment is reachable from both the endpoints(Source-db, replica-db).
* Run script.py using the below command:
   * python3 script.py
* script.py script will perform the below action:
   * Invoking "insert_values_source_db()" function to perform below actions:
   * Validating the connection with Source-db endpoint.
   * Checking if "values" key already exists or not, if yes then deleting the "values" key to reinitiate the "values" key.
   * Inserting the values 1-100 in "values" key.
   * Invoking the "reverse_values_repica_db()" function to retrive the values from "values" key in reverse order.
   * "reverse_values_repica_db()" will validate the connection with replica-db endpoint and also validate if "values" key present in replica-db or not. 
      If not, then check whether replication is working as expected or not.
   * "reverse_values_repica_db()" will print all the values in "values" key in reverse order.


## TROUBLESHOOTING
------------------
* Connection issue with source-db or replica-db:
   * Validate the endpoint's url, port and password.
   * Validate the endpoints are reachable from your IDE environment.

