### Components of HBase

#### Write Ahead Logs
* When any write happen in Hbase, HTable.put(Put)
  * Data is written in WAL and then it goes into Memstore.
  * In WAL data is shared across the HRegions hence the entry in WAL look like below.
    * HLogKey instance represents the key, and the key-value represents the rowkey, column family, column qualifier, timestamp, type, and value along with the region and table name where data needs to be stored
    * It rotates the log file when it becomes 90 percent of the block size, if set to 0.9.
  * WAL file is resides on HDFS hence its replicated on various data nodes.
  * it saves the data directly to the shared WAL and also keeps track of the changes by incrementing the sequence numbers for each edit
    * Since the WAL is an immutable way storage
  * Atomicity is guaranteed by wrapping all updates that comprise multiple columns into a single WALEdit instance and writing it in a
    single operation.
  * created in a directory called WALs under the root directory defined by the hbase.rootdir
    * also contains a subdirectory for each HRegionServer

```
Hbase Directory looks like below in HDFS path (hbase.rootdir)
/WALs/<region>/
/data/default/<table>/

Note : In case of terminal output file in gitrepo , ref directory:
  /usr/local/var/hbase/data/default/books/.tabledesc
 
```

#### HFile : actual data stored in this file in Disk of DataNode
* The files contain a variable number of data blocks and a fixed number of file info blocks and trailer blocks. The index blocks records the offsets of the data and meta blocks. Each data block contains a magic header and a number of serialized KeyValue instances
* Ref Hbase Directory mentioned above
  * Each table directory contains a file called .tableinfo within the .tabledesc folder.
  * Each table directory also has a separate directory for every region comprising the table, and the name of this directory is created using the MD5 hash portion of a region name
* You can check the terminal output for more data verification.
