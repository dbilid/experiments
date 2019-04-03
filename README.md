
# PARJ Experiments
This page contains pointers to material in order to reproduce the experiments for our paper "Scalable Parallelization of RDF Joins on MulticoreArchitectures" EDBT 2019.

In order to use the latest version of PARJ for importing and querying other datasets please see instructions at https://github.com/dbilid/PARJ

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

PARJ has been tested in DEBIAN 8 and UBUNTU 16.04 and 18.04.

### Prerequisites
-JAVA 8 with JAVA_HOME environment variable set. (e.g. sudo apt install openjdk-8-jdk)
set default version (sudo update-alternatives --config java)
and set JAVA_HOME: (e.g. JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/"
export JAVA_HOME)

-build-essential (e.g. sudo apt-get install build-essential)

-libgoogle-perftools-dev (e.g. sudo apt-get install  libgoogle-perftools-dev)

-pkg-config (e.g. sudo apt-get install pkgconf)

-libgtk2 (e.g. sudo apt-get install libgtk2.0-dev)

-libsqlite3-dev (e.g. sudo apt-get install libsqlite3-dev)

-libraptor2-dev (e.g. sudo apt-get install libraptor2-dev)

### Compile PARJ as SQLite Loadable extension:
Run:

wget godel.di.uoa.gr:8080/parj/experiments/importer.c

gcc -O3 -o importer.so importer.c -lpthread -lraptor2 -fPIC -shared \`pkg-config --cflags --libs glib-2.0\`;


### Run
-Download PARJ JAVA wrapper (e.g. wget godel.di.uoa.gr:8080/parj/experiments/parj.tar.gz)

-untar (e.g. tar -xzvf parj.tar.gz)

-Move PARJ SQLite loadable extension to PARJ directory:
mv importer.so parj/ 

-change to directory (cd parj) and run: java -cp "exareme-master-0.1-SNAPSHOT.jar:exareme-utils-0.1-SNAPSHOT.jar:external/*" madgik.exareme.master.importer.QueryTester /path/to/directory/

where /path/to/directory/ is the path where you have downloaded and extracted one of the databases used in evaluation

On startup you will be asked to provide the following information:

-Load Dictionary in memory: If yes the ID to URI dictionary will be loaded in memory. If no it will be kept on disk. This setting does not control if dictionary lookups will be finally added to the query. This option is controlled by the next setting.

-Use dictionary lookups for results (includes result tuple construction): If yes dictionary lookups will be performed during query execution. If dictionary is loaded in memory according to the previous setting, then memory lookups will be performed, otherwise disk will be accessed. If disk is accessed you can expect a big difference between cold cache and warm cache times. This option does not affect result printing, something that is controlled by next option.

-Print results: If yes results will be printed. If dictionary lookups are enabled then the URIs and literals will be printed, otherwise the number codes will be printed.

-Execute queries from File: If yes, after data loading you will be asked to provide the filepath of the file that contains the queries. Each query must be in a single line in the file. Lines with less than 30 characters will be ignored. Each query will be executed 11 times. The last 10 times will be taken into consideration for the average execution time. After all queries in the file have been executed the average execution time for each query, as well as the total average and geomean will be printed. If this setting is no, then you will be asked to directly give as input a query text in a single line (that is query text must not contain new line characters). After execution the number of results and total execution time in ms will be printed and you will be asked to give another query for execution.

-give number of threads: Insert the number of threads that would be used for each query

## Execution Times including dictionary lookups and tuple contruction

### lubm10240 32 threads

[802, 385, 647, 11, 5, 7, 473, 1326, 4387, 1459]

geo mean: 223.33807570399932

avg.: 950.2

no of results:[2528, 11058812, 0, 10, 10, 125, 450539, 2528, 4210245, 2278324]


### watdiv 1000 32 threads

[10, 7, 6, 6, 10, 48, 4, 3, 5, 2, 2, 6, 9, 12, 7, 22, 8, 10, 18, 133, 9, 7, 15, 4, 9, 7, 11, 19, 4, 5, 6, 3, 50360, 74207, 6812, 187322, 14224, 15493, 3, 3, 7, 6, 5, 4, 238, 6, 15, 32, 254, 22]

geo mean: 24.5253299467

avg.: 6988.8

no of results:[6, 1892, 12, 620, 2646, 4, 144, 0, 13, 100, 8, 0, 42, 6, 13, 185, 36, 111, 14, 4335801, 21308, 18557, 14609, 0, 1226, 1216, 18578, 23995, 202, 341, 1057, 5, 312548533, 353256708, 50018816, 1598301522, 76171155, 76171155, 447, 0, 0, 0, 1148, 571, 0, 252, 0, 17257, 0, 34736]

# Further experiments not included in the paper

## YAGO Dataset
Yago Dataset and Queries as found in paper Abdelaziz et. al "A survey and experimental comparison of distributed SPARQL engines for very large RDF data"

### Yago 32 Threads (silent mode) - Memory usage: 7.5 GB
[15, 17, 28, 222]
geo mean: 35.48238440211353
avg.: 70.5
no of results:[17, 0, 605993, 226]

### Yago 32 Threads (including dictionary lookups and tuple contruction) - Memory usage:12 GB
[13, 14, 139, 243]
geo mean: 49.793552903804596
avg.: 102.25
no of results:[17, 0, 605993, 226]




