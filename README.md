# Write-optimize-B-tree
In Today most of application require more insert than updates. So For this kind of application we can make write more optimize. In this we need make sure that writes should execute efficiently. We make sure that write is being done at immediate level we need not to take it from the next level before insertion. But In this case our select query can take time.

# Approach
So whenever a tuple comes we store the data in a table but after a certain table at level 1 will get filled so we need to partition it in level 2. Also we need to ensure that level 2 partition have large size than level.
So Each time when T1 get full then we need to send data to T2,then T3 and so on Now to implement this we need use table inheritance.
 In table inheritance when we insert into base table T, data actually gets inserted into either of its base tables.
Similarly for select queries, data is fetched not from T but from its corresponding child tables.
Whenever user submits a query on base table, we will be storing his insert data into child table which inherits the properties of base table. But before inserting it into child table we
are verifying if the size of table has reached a threshhold size or not.
If size reached threshhold then we are copying the records of that base table into another base table at next level and deleting the records from first base table or merging the records of previous level table and next level table into second next level table (since 2 tables are present at next level)
It is being assumed that each level has 2 tables.
Consider level 2- if T1+T2.a OR T1+T2.b size is more than available in tables then do the above functionality for level 3 now and records will now be entered in T2.a or T2.b instead of T1.
Similarly continue at every level.
