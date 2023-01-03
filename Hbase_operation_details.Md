# Details of Hbase operation
* All operations that mutate data are guaranteed to be atomic on a per-row basis
  * it does not matter if another client or thread is reading from or writing to the same row: they either read a consistent last mutation, or may have to wait before being able to apply their change
  * It also does not matter how many columns are written for the particular row; all of them are covered by this guarantee of atomicity.
* Each PUT operation is RPC call
  * You can club the put operation by using
    * ```table.setAutoFlush(false) :  flag on table this will club the put operation```
    * Use this when you have multiple writes and want to avoid wire transfer for every write
    * Put in- stances you stored are kept in memory in your client process. When you want to force the data to be written
      * ```flushCommits() method ships all the modifications to the remote server```
      * client is smart enough to batch these updates accordingly and send them to the appropriate region server, this mean row is directed to correct region server even if you have put as a job
      * force a flush of the buffer, this is usually not necessary, as the API tracks how much data you are buffering by counting the required heap size of every instance you have added
        * ```void setWriteBufferSize(long writeBufferSize) : default size is a moderate 2 MB ```
      * buffer is only ever flushed on two occasions :
        * Explicit flush
        * Implicit flush
          * call put()
          * setWriteBufferSize()
          * above both : compare the currently used buffer size with the configured limit and optionally invoke the flushCommits()
        * unconditionally is the close() method of HTable
    * When server or process get killed, the memory put data will get destroyed. you will not be able to get data since hbase server did not get it.
    * Performance tuning :
      * https://www.vskills.in/certification/tutorial/configuring-and-deploying/
      * http://hadoop-hbase.blogspot.com/2012/09/hbase-client-timeouts.html
    * Some Deep insides :
      * https://stackoverflow.com/questions/61856190/why-hbase-rows-are-said-to-be-stored-as-lexicographically-sorted
      * https://stackoverflow.com/questions/22528859/hbase-scan-performance
    * checkAndPut() call: 
      * only update if another value is not already present. This is achieved by setting the value parameter to null. In that case, the operation would succeed when the specified column is nonexistent
  * GET Method :
    * Both has a list of GET, List of PUT method , list of put can apply the valid one and return if invalid put is supplied with  error but at least valid put get applied.
      * In case of list of GET, not a single record is return, entire GET of list is get failed.
    * Sometime, we need to get the specified row or before that row if not present like in treeSet(Ceiling): ```getRowOrBefore(byte[] row, byte[] family)```
    * Methods :
      * boolean exists(Get get)
      * Result[] get(List<Get> gets)
      * List<KeyValue> getColumn(byte[] family, byte[] qualifier) 
      * KeyValue getColumnLatest(byte[] family, byte[] qualifier) 
      * boolean containsColumn(byte[] family, byte[] qualifier)
      * byte[] getValue(byte[] family, byte[] qualifier) byte[] value()
      *  byte[] getRow()
      *  int size()
      *  boolean isEmpty() KeyValue[] raw() List<KeyValue> list()