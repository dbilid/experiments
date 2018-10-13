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


