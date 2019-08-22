# PostgreSQL Basics: Manage Database

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
* UPDATE JOIN
* DELETE
* UPSERT


### Manage Tables
* CREATE TABLE

        // create a new table with the structure of another existing table
        CREATE TABLE link_tmp (LIKE link);
