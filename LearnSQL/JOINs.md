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



### SELF JOIN: INNER JOIN the same table
* Add AND to avoid self-matching of SELF JOIN

        SELECT * 
        FROM table_1 t1
        INNER JOIN table_2 t2
        ON t1.key_col=t2.key_col
        AND m1.to_avoid_col != m2.to_avoid_col;


