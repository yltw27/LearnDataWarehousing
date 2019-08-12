# PostgreSQL

* PostgreSQL, as the most advanced open source database, is so flexible that can serve as the folllowing solutions, and you can also integrate it with several analytics tools
    - a simple relational database
    - a time-series data database
    - an efficient and low-cost data warehouse

* Query Data
    * SELECT

        SELECT
            col_1,
            col_2
        FROM
            table_name;
        - Avoid using * since retrieving all columns from the table increases the traffic between the database and application layers. As a result, your applications will be slow and less scalable
        - Here is an example to SELECT with expressions ( || -> concatenation operator)

        SELECT 
            first_name || ' ' || last_name AS full_name,
            email
        FROM 
            customer;

    * ORDER BY (use ASC by default)

        SELECT
            col_1,
            col_2
        FROM
            table_name
        ORDER By
            col_1 ASC,
            col_2 DESC;
        - PostgreSQL allows you to sort rows based on the columns that even does not appear in the selection list

    * SELECT DISTINCT

        SELECT
            DISTINCT col_1, col_2
        FROM
            table_name;
        - To remove duplicate rows from the result set

        SELECT
            DISTINCT ON (col_1) col_alias,
            col_2
        FROM
            table_name
        ORDER BY
            col_1,
            col_2;
        - Notice that the DISTINCT ON expression must match the leftmost expression in the ORDER BY clause


* Create a schema

        CREATE SCHEMA mailchimp
    
    * There are 2 schema definitions
        1. How the tables and fields in a database are related to each other
        2. A folder for database tables
    * MySQL databases don’t support schema, so you may want to use a naming convention to name the tables you import, such as mailchimp_contacts
