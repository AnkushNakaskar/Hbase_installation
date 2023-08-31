# Hbase_installation
This project explain the Hbase installation and details
* Pre-requisite for Hbase installation 
  * Install Hadoop : Refer : https://github.com/AnkushNakaskar/springhadoophdfs
  * Install Zookeeper : https://www.datageekinme.com/general/setup/setting-up-my-mac-zookeeper/
      ```
      brew install zookeeper
      zkServer start
      ```
  * Now install Hbase :
    * using 
      ```
      brew install hbase
      brew services restart hbase
      ```
    * verify the Hbase installation
      ```
      hbase shell
      ```
    * Hmaster Web UI : http://localhost:16010/master-status  
      
* Following the simple way to check the Hbase table creation & table operations :
  * https://ashwani-singh-nitk.medium.com/hbase-installation-on-mac-505b90dd1635



### Hbase Request flow : most important to understand Hbase internal structure
* **How table is store in Hbase ?**
  * Table is divided into small chunk called regions
  * Each region hold the number of rows( like 1-5 rows with all the columns). 
    * **Single row cannot be part of multiple regions**
  * Structure of Hfile look like as below.
    * ```
      1. /table/region-id/column-family1/[list of HFiles]
      2. /table/region-id/column-family2/[list of HFiles]
      ```
    * When reading, the Scanner (which reads the data) ensures that it takes into account all HFiles while reading a data for a row key and a given column family.
      * Read it for more ref : https://stackoverflow.com/questions/22732179/hbase-and-hfiles-how-does-it-store-the-columns-family
  * So when client want to access the particular row ?
    * It first get the hbase:meta info from zookeeper and get the details for HRegions and HRegionServer details
    * meta table hold the info in below key format
      * ```
        structure of the hbase:meta table.
        Key—the region key of the format ([table],[region start key],[region id]). 
        A region with an empty start key is the first region in a table. 
        ```
    * Once the HRegionServer is accessible , it goes to HRegion and we can go to that path mention in structure of HFile location.
    * So for particular row, it scan all the column families and all the HFile of those column families.
    * Scanning single HFile is easy since data inside it , sorted based on rowKey.
    * These HFiles are immutable, and sorted.
      * So Data from a single column family for a single row need not be stored in the same HFile. So, this is true.



* Articles to refer or must read for Hbase:
  * https://towardsdatascience.com/hbase-working-principle-a-part-of-hadoop-architecture-fbe0453a031b
  * https://blog.cloudera.com/apache-hbase-write-path/
  * https://stackoverflow.com/questions/47688117/hbase-when-particular-region-server-fails-read-the-data-from-the-replicated-clu
  * https://stackoverflow.com/questions/11658328/when-does-hbase-actually-delete-a-row
  * https://www.syncfusion.com/succinctly-free-ebooks/hbase/inside-the-region-server#:~:text=The%20BlockCache%20is%20a%20read,contains%20the%20data%20on%20disk.
  * https://stackoverflow.com/questions/22732179/hbase-and-hfiles-how-does-it-store-the-columns-family
