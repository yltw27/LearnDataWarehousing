# PostgreSQL: Manage Tables

### Modify Data
* INSERT
    
        INSERT INTO table (column1, column2, …)
        VALUES
            (value1, value2, …),
            (value1, value2, …) ,...;

        // insert a row and return the index
        INSERT INTO link (url, NAME, last_update)
        VALUES('http://www.postgresql.org','PostgreSQL',DEFAULT) 
        RETURNING id;

        // to insert data from another table
        INSERT INTO table(column1,column2,...)
        SELECT column1,column2,...
        FROM another_table
        WHERE condition;

    * PostgreSQL provides a value for the serial column automatically so you do not and should not insert a value into the serial column. (e.g. index)

    * Use **'** as an escape character

            INSERT INTO link (url, name)
            VALUES
                ('http://www.oreilly.com','O''Reilly Media');

* UPDATE

        UPDATE table
        SET column1 = value1,
            column2 = value2 ,...
        WHERE condition;
 
        // update data from another table
        UPDATE link_tmp
        SET rel = link.rel,
            description = link.description,
            last_update = link.last_update
        FROM
            link
        WHERE
            link_tmp.id = link.id;

        // update with returning clause
        UPDATE link
        SET description = 'Learn PostgreSQL fast and easy',
            rel = 'follow'
        WHERE
            ID = 1 
        RETURNING id,
                description,
                rel;

    * The columns that are not on the list retain their original values.

    * To join to another table in the UPDATE statement, you specify the joined table in the FROM clause and provide the join condition in the WHERE clause. The FROM clause must appear immediately after the SET clause.

* DELETE

        DELETE FROM table
        WHERE condition;

        DELETE FROM table
        USING another_table
        WHERE table.id = another_table.id AND …

        // delete all rows from a table
        DELETE FROM link;
        // or you can use TRUNCATE
        TRUNCATE TABLE persons;

        // delete and show all rows
        DELETE FROM link_tmp 
        RETURNING *;

* UPSERT
    
        INSERT INTO table_name(column_list) VALUES(value_list)
        ON CONFLICT target action;

    * The target can be:
        * a column name
        * a WHERE clause
        * a constraint name

    * The action can be:
        * `DO NOTHING`
        * `DO UPDATE SET column_1 = value_1, .. WHERE condition`

            INSERT INTO customers (name, email)
            VALUES( 'Microsoft',
                    'hotline@microsoft.com' ) 
            ON CONFLICT (name) 
            DO
                UPDATE
                SET email = EXCLUDED.email || ';' || customers.email;

    * When you insert a new row into the table, PostgreSQL will update the row if it already exists, otherwise, PostgreSQL inserts the new row. (update + insert)

#### Transactions
* A database transaction is a single unit of work which may consist of one or more operations. E.g. A transfer from one bank account to another. A complete transaction must ensure subtracting an amount from the sender’s account and adding that same amount to the receiver’s account.

* To start a transaction, you use one of the following statements:

        BEGIN TRANSACTION;
        BEGIN WORK;
        BEGIN;

* To make the change become visible to other sessions (or users) you need to commit the transaction by using one of the following statements:

        COMMIT TRANSACTION;
        COMMIT WORK;
        COMMIT;

* To roll back or undo the change of the current transaction:

        ROLLBACK TRANSACTION;
        ROLLBACK WORK;
        ROLLBACK;

#### Import and Export Data

        COPY persons(first_name,last_name,dob,email)  // headers of the csv file
        FROM 'C:\tmp\persons.csv' DELIMITER ',' CSV HEADER;

        COPY persons 
        TO 'C:\tmp\persons_db.csv' DELIMITER ',' CSV HEADER;

-----

### Manage Tables
* CREATE TABLE

        CREATE TABLE table_name (
            column_name TYPE column_constraint,
            table_constraint table_constraint
        ) INHERITS existing_table_name;

    * column_constraint
        * NOT NULL
        * UNIQUE
        * PRIMARY KEY
        * CHECK
        * REFERENCES (use REFERENCES to define the foreign key constraint)

                CREATE TABLE account(
                    user_id serial PRIMARY KEY,
                    username VARCHAR (50) UNIQUE NOT NULL,
                    password VARCHAR (50) NOT NULL,
                    email VARCHAR (355) UNIQUE NOT NULL,
                    created_on TIMESTAMP NOT NULL,
                    last_login TIMESTAMP
                );


    * table_constraint: a table-level constraint that defines rules for the data in the table
    * INHERITS: Specify an existing table from which the new table inherits. It means the new table contains all columns of the existing table and the columns defined in the CREATE TABLE statement. This is a PostgreSQL’s extension to SQL.

    * To create a new table with the structure of another existing table

            CREATE TABLE link_tmp (LIKE link);

* SELECT INTO

        SELECT
            film_id,
            title,
            rental_rate
        INTO TABLE film_r
        FROM
            film
        WHERE
            rating = 'R'
        AND rental_duration = 5
        ORDER BY title;