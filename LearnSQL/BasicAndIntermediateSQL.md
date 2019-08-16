# Basic and Intermediate SQL

Based on 
1. [Mode: SQL Tutorial](https://mode.com/sql-tutorial/)
2. [DataCamp: Joining Data in SQL](https://www.datacamp.com/courses/joining-data-in-postgresql)

### LIKE

        SELECT *
        FROM tutorial.billboard_top_100_year_end
        WHERE "group" LIKE 'Snoop%'

* "group" appears in quotations above because GROUP is actually the name of a function in SQL. The double quotes are a way of indicating that you are referring to the column name "group", not the SQL function. In general, putting double quotes around a word or phrase will indicate that you are referring to that column name.
* ILIKE: Case-insensitive
        
### IS NULL

        SELECT * 
        FROM tutorial.billboard_top_100_year_end
        WHERE song_name IS NULL;

* **WHERE artist = NULL** will not work since you can’t perform arithmetic on null values.

-----


### INNER JOIN
* When the joined columns have the same name in different tables, we could use USING instead of ON

        SELECT  left_table.id left_id,
                left_table.val left_val,
                right_table.val right_val
        FROM left_table
        INNER JOIN right_table
        USING (id);

* SELF JOIN: INNER JOIN the same table
    * Add AND to avoid self-matching of SELF JOIN

            SELECT * 
            FROM table_1 t1
            INNER JOIN table_2 t2
            ON t1.key_col=t2.key_col
            AND m1.to_avoid_col != m2.to_avoid_col;

* CASE, WHEN and THEN: Create a new column with conditions

            SELECT name, continent, code, surface_area,
                CASE WHEN surface_area > 2000000 THEN 'large'
                WHEN surface_area > 350000 THEN 'medium'
                ELSE 'small' END
                AS geosize_group
            FROM countries;

* INTO: Save the result as another table

        SELECT country_code, size,
            CASE WHEN size > 50000000 THEN 'large'
                WHEN size > 1000000 THEN 'medium'
                ELSE 'small' END
                AS popsize_group
        INTO pop_plus       
        FROM populations
        WHERE year = 2015;
