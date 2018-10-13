# PARJ Experiments

## PARJ Databases used in evaluation

[WatDiv 1000](http://godel.di.uoa.gr:8080/parj/experiments/parjwatdiv1000.tar.gz)

[LUBM 10240](http://godel.di.uoa.gr:8080/parj/experiments/parjlubm10240.tar.gz)

[LUBM 5120](http://godel.di.uoa.gr:8080/parj/experiments/parjlubm5120.tar.gz)

[LUBM 2560](http://godel.di.uoa.gr:8080/parj/experiments/parjlubm2560.tar.gz)

[LUBM 1280](http://godel.di.uoa.gr:8080/parj/experiments/parjlubm1280.tar.gz)

## Queries

[WatDiv queries](http://godel.di.uoa.gr:8080/parj/experiments/watdiv.q)

[LUBM queries](http://godel.di.uoa.gr:8080/parj/experiments/lubm.q)



## Running PARJ

Currently we provide [precompiled binaries](http://godel.di.uoa.gr:8080/parj/experiments/parj.tar.gz) for 64 bit linux. Source code and instructions to build will be available soon. PARJ has been tested in DEBIAN 8 and UBUNTU 16.04 and 18.04.

### Prerequisites
-JAVA 8 with JAVA_HOME environment variable set. 

-google-perftools (e.g. sudo apt-get install google-perftools)

### Run
-Download precompiled binaries (e.g. wget godel.di.uoa.gr:8080/parj/experiments/parj.tar.gz)

-untar (e.g. tar -xzvf parj.tar.gz)

-change to directory (cd parj) and run: java -cp "exareme-master-0.1-SNAPSHOT.jar:exareme-utils-0.1-SNAPSHOT.jar:external/*" madgik.exareme.master.importer.QueryTester /path/to/directory/ 

where /path/to/database/ is the path where you have downloaded and extracted one of the databases used in evaluation

On startup you will be asked to provide the following information:

-Load Dictionary in memory: If yes the ID to URI dictionary will be loaded in memory. If no it will be kept on disk. This setting does not control if dictionary lookups will be finally added to the query. This option is controlled by the next setting.

-Use dictionary lookups for results (includes result tuple construction): If yes dictionary lookups will be performed during query execution. If dictionary is loaded in memory according to the previous setting, then memory lookups will be performed, otherwise disk will be accessed. If disk is accesed you can expect a big difference between cold cache and warm cache times. This option does not affect result printing, something that is controlled by next option.

-Print results: If yes results will be printed. If dictionary lookups are enabled then the URIs and literals will be printed, otherwise the number codes will be printed.

-Execute queries from File: If yes, after data loading you will be asked to provide the filepath of the file that contains the queries. Each query must be in a single line in the file. Lines with less than 30 characters will be ignored. Each query will be executed 11 times. The last 10 times will be taken into consideration for the average execution time. After all queries in the file have been executed the average execution time for each query, as well as the total average and geomean will be printed. If this setting is no, then you will be asked to directly give as input a query text in a single line (that is query text must not contain new line characters). After execution the number of results and total execution time in ms will be printed and you will be asked to give another query for execution.

-give number of threads: Insert the number of threads that whould be used for each query
