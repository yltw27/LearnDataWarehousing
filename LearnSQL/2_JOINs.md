# SQL JOINs

The real power of SQL comes from working with data from multiple tables at once

Based on 
1. [Mode: SQL Tutorial](https://mode.com/sql-tutorial/)
2. [DataCamp: Joining Data in SQL](https://www.datacamp.com/courses/joining-data-in-postgresql)


### INNER JOIN
* When the joined columns have the same name in different tables, we could use USING instead of ON

        SELECT  left_table.id left_id,
                left_table.val left_val,
                right_table.val right_val
        FROM left_table
        INNER JOIN right_table
        USING (id);

* INTO: Save the result as another table

        SELECT country_code, size,
            CASE WHEN size > 50000000 THEN 'large'
                WHEN size > 1000000 THEN 'medium'
                ELSE 'small' END
                AS popsize_group
        INTO pop_plus       
        FROM populations
        WHERE year = 2015;


### LEFT JOIN/ RIGHT JOIN
* The LEFT JOIN/RIGHT JOIN command tells the database to **return all rows in the table in the FROM clause**, regardless of whether or not they have matches in the table in the LEFT/RIGHT JOIN clause.
* JOIN tables on multiple foreign keys could help to enhance accuracy and/or performance.

![PostgreSQL JOINs](attachments/PostgreSQL-Joins.png)


### UNION
* SQL joins allow you to combine two datasets side-by-side, but UNION allows you to stack one dataset on top of the other.
* Note that UNION only appends **distinct** values.
* If you’d like to append all the values from the second table, use **UNION ALL**. You’ll likely use UNION ALL far more often than UNION. 
* SQL has strict rules for appending data:
    1. Both tables must have the same number of columns
    2. The columns must have the same data types in the same order as the first table
* No need to use aliases for table name in UNION since there're 2 independent FROM

        SELECT *
        FROM table_ame
        UNION ALL
        SELECT *
        FROM another_table_name;;


### SELF JOIN: INNER JOIN the same table
* Add AND to avoid self-matching of SELF JOIN

        SELECT * 
        FROM table_1 t1
        INNER JOIN table_2 t2
        ON t1.key_col=t2.key_col
        AND m1.to_avoid_col != m2.to_avoid_col;
