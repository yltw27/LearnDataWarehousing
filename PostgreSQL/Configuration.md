# Configuration
* Here are some tips to configure your PostgreSQL database to work as a data warehouse in the correct way: 
    * Memory based
        - max_connections: As a data warehouse database, you don’t need a high amount of connections because this will be used for reporting and analytics work, so you can limit the max connections numbers using this parameter
        - shared_buffers: Sets the amount of memory that the database server uses for shared memory buffers. A reasonable value can be from 15% to 25% of the RAM memory
        - effective_cache_size: This value is used by the query planner to take into account plans that may or may not fit in memory. This is taken into account in the cost estimates of using an index; a high value makes it more likely that index scans are used and a low value makes it more likely that sequential scans will be used. A reasonable value would be around 75% of the RAM memory
        - work mem: Specifies the amount of memory that will be used by the internal operations of ORDER BY, DISTINCT, JOIN, and hash tables before writing to the temporary files on disk. When configuring this value we must take into account that several sessions are executing these operations at the same time and each operation will be allowed to use as much memory as specified by this value before it starts to write data in temporary files. A reasonable value can be around 2% of the RAM Memory
        - maintenance_work_mem: Specifies the maximum amount of memory that maintenance operations will use, such as VACUUM, CREATE INDEX, and ALTER TABLE ADD FOREIGN KEY. A reasonable value can be around 15% of the RAM Memory

    * CPU Based
        - Max_worker_processes: Sets the maximum number of background processes that the system can support. A reasonable value can be the number of CPUs
        - Max_parallel_workers_per_gather: Sets the maximum number of workers that can be started by a single Gather or Gather Merge node. A reasonable value can be 50% of the number of CPU
        - Max_parallel_workers: Sets the maximum number of workers that the system can support for parallel queries. A reasonable value can be the number of CPUs
        - As the data loaded into our data warehouse shouldn’t change, we can also set the Autovacuum in off to avoid an extra load on your PostgreSQL database. The Vacuum and Analyze processes can be part of the batch load process
