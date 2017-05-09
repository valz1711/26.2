# 26.2
1 Bucketing
• Bucketing concept is based on (hashing function on the bucketed column) mod (by total number of buckets). The hash_function depends on the type of the bucketing column.
• Records with the same bucketed column will always be stored in the same bucket.
• We use CLUSTERED BY clause to divide the table into buckets.
• Physically, each bucket is just a file in the table directory, and Bucket numbering is 1-based.
• Bucketing can be done along with Partitioning on Hive tables and even without partitioning.
• Bucketed tables will create almost equally distributed data file parts, unless there is skew in data.
• Bucketing is enabled by setting hive.enforce.bucketing = true;
• Bucketed tables offer efficient sampling than by non-bucketed tables. With sampling, we can try out queries on a fraction of data for testing and debugging purpose when the original data sets are very huge.
• As the data files are equal sized parts, map-side joins will be faster on bucketed tables than non-bucketed tables.
• Bucketing concept also provides the flexibility to keep the records in each bucket to be sorted by one or more columns. This makes map-side joins even more efficient, since the join of each bucket becomes an efficient merge-sort.


2 Bucketing vs partitioning
• Partitioning helps in elimination of data, if used in WHERE clause, where as bucketing helps in organizing data in each partition into multiple files, so that the same set of data is always written in same bucket.
• Bucketing helps a lot in joining of columns.
• Hive Bucket is nothing but another technique of decomposing data or decreasing the data into more manageable parts or equal parts.
• For example we have table with columns like date, employee_name, employee_id, salary, leaves etc .
• In this table just use date column as the top-level partition and the employee_id as the second-level partition leads to too many small partitions.
• We can use HASH value for bucketing or a range to bucket the data.

3 partitioning
• Hive organizes tables horizontally into partitions.
• It is a way of dividing a table into related parts based on the values of partitioned columns such as date, city, department etc.
• Using partition, it is easy to query a portion of the data.
• Partitioning can be done based on more than column which will impose multi-dimensional structure on directory storage.
• In Hive, partitioning is supported for both managed and external tables.
• The partition statement lets Hive alter the way it manages the underlying structures of the table’s data directory.
• In case of partitioned tables, subdirectories are created under the table’s data directory for each unique value of a partition column.
• When a partitioned table is queried with one or both partition columns in criteria or in the WHERE clause, what Hive effectively does is partition elimination by scanning only those data directories that are needed.
• If no partitioned columns are used, then all the directories are scanned (full table scan) and partitioning will not have any effect.
