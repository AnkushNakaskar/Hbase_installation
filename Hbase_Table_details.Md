# Details of Hbase table structure
* Table is  like below :
  * Table is part of namespace , like we have database in SQL (https://stackoverflow.com/questions/45984860/what-is-more-efficient-in-performance-of-hbase-multiple-tables-of-same-structure)
    * ```
       Once a namespace is created and a table is added to it, the path on HDFS will look like the following
       <ROOT PATH>/data/<NAMESPACE NAME>/<TABLE NAME>```
    * Row -> Row_Key 
      * Row -> Column Family -> Column
      * You can access row using row_key, which is like a primary key
      * Table look like SQL table form, but internally it stored in columnar way(Column Family)
      * Each cell can store upto 10- 15 MB, Data does not have any types 
        * Every value is stored as byte array, so we can store any object which is serializable
    * Column Family must be decided at the time of table creation, we cant modify or add or remove it at any point
      * While we can add column at any point in time
    * Default value for version is 3, that mean each value can be of 3 versions
  * Operations in tables are
    * GET
      * It is similar to the select [fields] where RowKey=<Row Key value here>
    * PUT
      * adds a new row of data to a table or updates/overrides a specific row of data
    * DELETE
      * removes a row or a set of rows from a table
    * SCAN
      * used to read multiple rows of data in contrast to Get where we need to specify a set of rows to read data
      * it is marked as tombstone, and once compaction takes place, the row is finally deleted or removed from a table.
    * We can change the number of version in two ways
      * One while creating table
      * One when we execute the alter query