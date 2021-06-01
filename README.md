# Sqoop-other-interview-questions
Import data from mysql to HDFS

To get data from mysql to HDFS  -> use import
To get data from HDFS to mysql -> use export

Sqoop: sqoop import --connect jdbc:mysql://localhost/movielens --driver com.mysql.jdbc.Driver --tables movies -m1
This m1 indicates total number of mappers. Here Mapper is 1.

To create a new directory in hive :
Sqoop: sqoop import --connect jdbc:mysql://localhost/movielens --driver com.mysql.jdbc.Driver --tables movies --hive tablename

Incremental Imports :
If we want to load data from surrogate key greater than the current date, then we have to use the below one:
sqoop import --connect jdbc:mysql://localhost/movielens --driver com.mysql.jdbc.Driver --tables movies --hive tablename --check-column --last -value

Sqoop for Export:
sqoop export --connect jdbc:mysql://localhost/movielens --driver com.mysql.jdbc.Driver --tables movies --export-dir /apps/hive/warehouse/movies --input-fields-terminated-by '\0001'

Sqoop Import :
Import specific database, specific tables from Relational databases to HDFS.
Sqoop Import all tables :


Connection of Sqoop in ITVERSITY :
Connect to MYSQL using mysql -u username -p 
Enter password : Password name
 mysql -u retail_user -h g02.itversity.com -p
Enter password:


List of commands :
sqoop eval --connect jdbc:mysql://ms.itversity.com/retail_db  --username retail_user  --password itversity   --query "SELECT count(1) from orders"
either this can be used :
sqoop eval --connect jdbc:mysql://ms.itversity.com/retail_db  --username retail_user  --password itversity   --e "SELECT count(1) from orders"
This command generally helps to run queries on the databases and check whether the import is working fine.

sqoop-list-databases 
sqoop-list-databases --connect jdbc:mysql://ms.itversity.com/retail_db --username retail_user  --password itversity
Sqoop-list-tables :
 sqoop-list-tables --connect jdbc:mysql://ms.itversity.com/retail_db --username retail_user  --password itversity
 
 Sqoop-import-all-tables : Imports all tables from mysql to hdfs. Below is the command:
 sqoop-import-all-tables --connect jdbc:mysql://ms.itversity.com/retail_db --username retail_user --password itversity --as-sequencefile -m12 --warehouse-dir /user/itv000076/sqoop
We cannot use --split-by, -where clause in the import statement.

Sqoop import table to hive table :
sqoop-import-all-tables --connect jdbc:mysql://ms.itversity.com/retail_db --username retail_user --password itversity --as-sequencefile -m12 --warehouse-dir /user/itv000076/sqoop --hive-import --hive-overwrite --create-hive-table --hive-table --hive-partition-key--hive-partition-value

Point to be noted : The sqoop job will fail - if mapper is set to more than 1, and splitby column is not mentioned and there is no primary key.

Incremental Imports : two types of Incremental Imports are : append and lastmodified
sqoop import --connect jdbc:mysql://ms.itversity.com/retail_db --username retail_user --password itversity --as-sequencefile --incremental append --check-column colname
--last-value 500

Splitby column to indicate the partition. 
Sqoop Supported Hive commands :
--map-column-hive, --hive-home, --hive-partition-key, --hive-partition-value
sqoop import --connect jdbc:mysql://ms.itversity.com/retail_db --username retail_user --password itversity --as-sequencefile --incremental lastmodified --check-column colname
--last-value lastmodifiedtimestamp


Next to learn: Sqoop-merge
sqoop-codegen
hcatalog
 
