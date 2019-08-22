# PostgreSQL: Manage Databases

* CREATE DATABASE [more](http://www.postgresqltutorial.com/postgresql-create-database/)

        CREATE DATABASE db_name
        OWNER =  role_name
        TEMPLATE = template
        ENCODING = encoding
        LC_COLLATE = collate
        LC_CTYPE = ctype
        TABLESPACE = tablespace_name
        CONNECTION LIMIT = max_concurrent_connection

* ALTER DATABASE [more](http://www.postgresqltutorial.com/postgresql-alter-database/)

        ALTER DATABASE target_database action;

        // rename database
        ALTER DATABASE target_database 
        RENAME TO new_database;

        // change owner
        ALTER DATABASE target_database 
        OWNER TO new_onwer;

    * To create a new owner

            CREATE ROLE hr
            VALID UNTIL 'infinity';

* DROP DATABASE

        DROP DATABASE [IF EXISTS] name;

    * Use IF EXISTS to prevent an error from removing a non-existent database. PostgreSQL will issue a notice instead.

* Copy a database
    * Copy a database to test some processes

            CREATE DATABASE dvdrental_test 
            WITH TEMPLATE dvdrental;

* Get size in PostgreSQL [more](http://www.postgresqltutorial.com/postgresql-database-indexes-table-size/)

        // get table size
        select pg_relation_size('actor');

        // make the result more human readable
        SELECT pg_size_pretty (pg_relation_size('actor'));

        // get the total size of a table,
        SELECT
            pg_size_pretty (
                pg_total_relation_size ('actor')
            );

        // get database size
        SELECT
            pg_database.datname,
            pg_size_pretty(pg_database_size(pd_database.datname)) AS size
        FROM pd_database;