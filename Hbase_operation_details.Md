# Details of Hbase operation
* All operations that mutate data are guaranteed to be atomic on a per-row basis
  * it does not matter if another client or thread is reading from or writing to the same row: they either read a consistent last mutation, or may have to wait before being able to apply their change
  * It also does not matter how many columns are written for the particular row; all of them are covered by this guarantee of atomicity.