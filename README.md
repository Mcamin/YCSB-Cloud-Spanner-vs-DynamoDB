DBaaS: A Comparison and Analysis of Cloud Spanner and DynamoDB Performances
====================================

Requirements:
------------------
  Java 1.7+  
  Maven3
 

Getting Started
---------------

1. Clone source code from github:

    ```
    git clone git@github.com:madtomy/YCSB.git
    ```
2. Build from source.
    ```
     mvn clean package
    ```  
3. Set up a database to benchmark.
  - DynamoDB:
  create table usertable with id as PRIMARY KEY.
  - CloudSpanner:
   create a database with the following schema:

```
CREATE TABLE usertable (
  id STRING(MAX),
  field0 STRING(MAX),
  field1 STRING(MAX),
  field2 STRING(MAX),
  field3 STRING(MAX),
  field4 STRING(MAX),
  field5 STRING(MAX),
  field6 STRING(MAX),
  field7 STRING(MAX),
  field8 STRING(MAX),
  field9 STRING(MAX),
) PRIMARY KEY(id);
```
4. For more details: See the README file under database directory for commands to run the workload.

Credits:
------------------------------
[YCSB](https://github.com/brianfrankcooper/YCSB)  



Building from source
--------------------

YCSB requires the use of Maven 3; if you use Maven 2, you may see [errors
such as these](https://github.com/brianfrankcooper/YCSB/issues/406).

YCSB requires the use of JDK and not JRE on Windows.

On windows, Make sure to add JDK as `JAVA_HOME`, 
and the maven, and jdk paths to the `Path` variable 
in your System variables

To build the cloudspanner database binding:

    mvn -pl com.yahoo.ycsb:cloudspanner-binding -am clean package

To build the dynamodb database binding:

    mvn -pl com.yahoo.ycsb:dynamodb-binding -am clean package

To build Both dynamodb and cloudspanner:
   
    mvn clean package


4. Run YCSB command. 

    On Linux:
    ```sh
    bin/ycsb.sh load basic -P workloads/workloada
    bin/ycsb.sh run basic -P workloads/workloada
    ```

    On Windows:
    ```bat
    bin\ycsb.bat load basic -P workloads\workloada
    bin\ycsb.bat run basic -P workloads\workloada
    ```
Workloads types
--------------------
- Workload%T%%N%:

   1- %T% : Workload Type .
   
   2- %N% : number of operations 
    performed is set to 10,000 in every test for number 1 and 20,000 for number 2.

- List of Workloads:
   1. Workloada1 or Workloada2
            Session Store: Read/update ratio: 50/50
            
   2. Workloadb2 or Workloadb2
            Session Store: 100 % Read Modify Write 
            
   3. Workloadc1 or Workloadc2
            Hadoop : Read Only. 100% Read
            
   4. Workloade1 or Workloade2
            Threaded conversations: Short ranges. 95% Scan, 5% Insert
            
   5. Workloadf1 or Workloadf2
            Logging: Blind Write. 100% Insert 

Load the Data(On Linux:)
--------------------
  1. DynamoDB service :
  ```
          bin/ycsb load dynamodb -P workloads/workloadb1 -p recordcount=5000000 -P ./dynamodb/conf/dynamodb.properties -threads 10 -s
   ```
   
  2. CloudSpanner service :
  ```
              ./bin/ycsb load cloudspanner -P cloudspanner/conf/cloudspanner.properties -P workloads/workloadb1 -p recordcount=5000000 -p cloudspanner.batchinserts=1000 -threads 10 -s
   ```

Run a Workload
--------------------
  1. DynamoDB service :
  ```
               bin/ycsb run dynamodb -P workloads/workloadb1 -p recordcount=5000000 -P ./dynamodb/conf/dynamodb.properties -threads 10 -s  
  ``` 
           
  2. CloudSpanner service :
  ```
              bin/ycsb run cloudspanner -P cloudspanner/conf/cloudspanner.properties -P workloads/workloadb1 -p recordcount=5000000 -p operationcount=10000 -threads 10 -s >>~/Spanner/5M/workloadb1-1.csv
  ```
Additional Links:
-------------------------------
  The official YCSB wiki has lot of informative material on running workloads and different parameters available.

  See [Running workload](https://github.com/brianfrankcooper/YCSB/wiki/Running-a-Workload)
  for a detailed documentation on how to run a workload.

  See [Core properties](https://github.com/brianfrankcooper/YCSB/wiki/Core-Properties) for
  the list of available workload properties.


