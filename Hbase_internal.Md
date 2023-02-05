* Hbase architecture in details :
  * Please ref the image ![](img/Hbase_architecture.png)
  * As image says : 
    * ```The HRegionServer opens the region and creates a corresponding HRegion object. When the HRegion is opened it sets up a Store instance for each HColumnFamily for every table as defined by the user beforehand. Each Store instance can, in turn, have one or more StoreFile instances, which are lightweight wrappers around the actual storage file called HFile. A Store also has a MemStore, and the HRegionServer a shared HLog in- stance ```