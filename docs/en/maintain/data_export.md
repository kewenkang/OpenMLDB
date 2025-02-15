# Data Export Tool

Data Export Tool locates in [src/tools](https://github.com/4paradigm/OpenMLDB/tree/main/src/tools)。It supports exporting data from remote machines in standalone mode or cluster mode.

## 1. Build

Generate the Unix Executable file：`make` under src folder.

## 2. Data Export Usage

### 2.1 Command Line Arguments

All configurations are showed as follows, * indicates required configurations.

```
Usage: ./data_exporter [--delimiter=<delimiter>] --db_name=<dbName> 
                     [--user_name=<userName>] --table_name=<tableName>
                     --config_path=<configPath>
      
*     --db_name=<dbName>          openmldb database name
*     --table_name=<tableName>    openmldb table name of the selected database
*     --config_path=<configPath>  absolute or relative path of the config file
      --delimiter=<delimiter>     delimiter for the output csv, default is ','
      --user_name=<userName>      user name of the remote machine
```

### 2.2 Important Configurations Instructions

Descriptions of the important configurations:

- `--db_name=<dbName>`: OpenMLDB database name. The database must exist, otherwise would return an error message: database not found.
- `--table_name=<tableName>`: table name. The table must exist in the selected database, otherwise would return an error message: table not found.
- `--config_path=<configPath]`: configuration file of the distrubution of OpenMLDB. The format of this file is yaml.

### 2.3 Example of the Config File:

     mode: cluster
     zookeeper:
         zk_cluster: 172.17.0.2:2181
         zk_root_path: /openmldb
     nameserver:
     - 
         endpoint: 172.17.0.2:6527
         path: /work/ns1
     - 
         endpoint: 172.17.0.2:6528
         path: /work/ns2
     tablet:
     - 
         endpoint: 172.17.0.2:10921
         path: /work/openmldb
     - 
         endpoint: 172.17.0.2:10922
         path: /work/openmldb

## 3. Error Handling

If data export fails, Glog would print possible causes of the errors.
