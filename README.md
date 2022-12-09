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
      
