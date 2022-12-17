#Details of Hbase table structure
* Table is  like below :
  * Row -> Row_Key 
    * Row -> Column Family -> Column
    * You can access row using row_key, which is like a primary key
    * Table look like SQL table form, but internally it stored in columnar way(Column Family)
    * Each cell can store upto 10- 15 MB, Data does not have any types 
      * Every value is stored as byte array, so we can store any object which is serializable 