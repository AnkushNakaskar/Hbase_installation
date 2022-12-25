# Details of Hbase operation
* All operations that mutate data are guaranteed to be atomic on a per-row basis
  * it does not matter if another client or thread is reading from or writing to the same row: they either read a consistent last mutation, or may have to wait before being able to apply their change
  * It also does not matter how many columns are written for the particular row; all of them are covered by this guarantee of atomicity.
* Each PUT operation is RPC call
  * You can club the put operation by using
    * ```table.setAutoFlush(false) :  flag on table this will club the put operation```
    * Use this when you have multiple writes and want to avoid wire transfer for every write