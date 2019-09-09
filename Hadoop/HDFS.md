# HDFS, Hadoop Distributed File System

### Benefits of HDFS
* Support distributed processing (blocks instead of whole files)
* Handle failures by replicating blocks
* Scalability (able to support future expansion)
* Cost effective (use commodity hardwares)

### HDFS Commands
* All HDFS commands start with **hadoop fs**
* List files under a dir `hadoop fs -ls /`
* Listing default to home directory `hadoop fs -ls` or `hadoop fs -ls /user/$USER` 
* Create a dir `hadoop fs -mkdir <newDir>`
* Copy from local `hadoop fs -copyFromLocal <from> <to>`
* Copy to local `hadoop fs -copyToLocal <from> <to>`
* Copy a file from HDFS to HDDFS `hadoop fs -cp <from> <to>`
* Move a file from HDFS to HDDFS `hadoop fs -mv <from> <to>`
* Change or set replication factor

        hadoop fs -Ddfs.replication=2 -cp hadoop-test2/dwp-payments-april10.csv hadoop-test2/test_with_rep2.csv

* Change permission `hadoop fs -chmod 777 <file>`
* File system check (requires admin previleges)

        sudo -u hdfs hdfs fsck /user/hirwuser150430/hadoop-test2 -files -blocks -locations 

    * Local system can only see the blocks, HDFS is responsible for managing and constructing the blocks into files.

### HDFS Architecture
* Datanode (slave node): Knows about the blocks and its locations it's responsible for
* Namenode (master node): Keeps track all the files of datasets in HDFS
* Configuration files are under /etc/hadoop/conf
    * core-site.xml
        * The location of namenode is saved as the value of **fs.defaultFS**
        * Any node can look up this file
    * hdfs-site.xml
        * dfs.namenode.name.dir: where namenode can store its files
        * dfs.datanode.data.dir: where datanode can store blocks and files
        * dfs.namenode.http-address
    * masters: specifies the secondary namenode
    * slaves: contains the list of all datanodes
* Rack: collection of nodes
