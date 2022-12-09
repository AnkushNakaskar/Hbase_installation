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


* Articles to refer or must read for Hbase:
  * https://towardsdatascience.com/hbase-working-principle-a-part-of-hadoop-architecture-fbe0453a031b
  * https://blog.cloudera.com/apache-hbase-write-path/
  * https://stackoverflow.com/questions/47688117/hbase-when-particular-region-server-fails-read-the-data-from-the-replicated-clu
  * https://stackoverflow.com/questions/11658328/when-does-hbase-actually-delete-a-row
