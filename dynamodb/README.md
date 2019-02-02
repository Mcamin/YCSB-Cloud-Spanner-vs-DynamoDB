## Quick Start

This section describes how to run YCSB on CouchDB.

## Configure

    YCSB_HOME - YCSB home directory
    DYNAMODB_HOME - Amazon DynamoDB package files

Please refer to https://github.com/brianfrankcooper/YCSB/wiki/Using-the-Database-Libraries
for more information on setup.

# Benchmark

    $YCSB_HOME/bin/ycsb load dynamodb -P workloads/workloada -P dynamodb.properties
    $YCSB_HOME/bin/ycsb run dynamodb -P workloads/workloada -P dynamodb.properties

# Properties

    $DYNAMODB_HOME/conf/dynamodb.properties
    $DYNAMODB_HOME/conf/AWSCredentials.properties

