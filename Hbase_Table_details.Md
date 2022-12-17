# Details of Hbase table structure
* Table is  like below :
  * Table is part of namespace , like we have database in SQL (https://stackoverflow.com/questions/45984860/what-is-more-efficient-in-performance-of-hbase-multiple-tables-of-same-structure)
    * Row -> Row_Key 
      * Row -> Column Family -> Column
      * You can access row using row_key, which is like a primary key
      * Table look like SQL table form, but internally it stored in columnar way(Column Family)
      * Each cell can store upto 10- 15 MB, Data does not have any types 
        * Every value is stored as byte array, so we can store any object which is serializable
    * Column Family must be decided at the time of table creation, we cant modify or add or remove it at any point
      * While we can add column at any point in time
      * 