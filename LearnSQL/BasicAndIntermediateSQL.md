# Basic and Intermediate SQL

Based on [Mode: SQL Tutorial](https://mode.com/sql-tutorial/)

### Basic SQL
* LIKE

        SELECT *
        FROM tutorial.billboard_top_100_year_end
        WHERE "group" LIKE 'Snoop%'

    * "group" appears in quotations above because GROUP is actually the name of a function in SQL. The double quotes are a way of indicating that you are referring to the column name "group", not the SQL function. In general, putting double quotes around a word or phrase will indicate that you are referring to that column name.
    * ILIKE: Case-insensitive
        
* IS NULL

        SELECT * 
        FROM tutorial.billboard_top_100_year_end
        WHERE song_name IS NULL;

    * **WHERE artist = NULL** will not work since you can’t perform arithmetic on null values.


### Imtermediate SQL
* SUM
    * Always use the same column in SUM() and COUNT() to calculate average values

            SELECT SUM(open)/COUNT(open)
            FROM tutorial.aapl_historical_stock_price;

* AVG
    * When AVG() is used, remember to filter NULL value out

            SELECT AVG(high)
            FROM tutorial.aapl_historical_stock_price
            WHERE high IS NOT NULL;

* HAVING: the “clean” way to filter a query that has been aggregated, but this is also commonly done using a subquery

* CASE, WHEN and THEN: Create a new column with conditions (分群)

            SELECT name, 
                    continent, 
                    code, 
                    surface_area,
                    CASE WHEN surface_area > 2000000 THEN 'large'
                        WHEN surface_area > 350000 THEN 'medium'
                        ELSE 'small' END AS geosize_group
            FROM countries;

    * The CASE column must appear in the GROUP BY clause or be used in an aggregate function

            SELECT CASE WHEN year IN ('FR', 'SO') THEN 'underclass'
                        WHEN year IN ('JR', 'SR') THEN 'upperclass'
                        ELSE 'unknown' END AS class_group,
                    SUM(weight)
            FROM benn.college_football_players
            GROUP BY 1;

    * GROUP BY [num] is a short version of GROUP BY [Column_name]
    * CASE WHEN could be used with aggregate functions

            SELECT state,
                COUNT(CASE WHEN year = 'FR' THEN 1 ELSE NULL END) AS fr_count,
                COUNT(CASE WHEN year = 'SO' THEN 1 ELSE NULL END) AS so_count,
                COUNT(CASE WHEN year = 'JR' THEN 1 ELSE NULL END) AS jr_count,
                COUNT(CASE WHEN year = 'SR' THEN 1 ELSE NULL END) AS sr_count,
                COUNT(1) AS total_players
            FROM benn.college_football_players
            GROUP BY state
            ORDER BY total_players DESC;

    * CASE WHEN and string comparison

            SELECT CASE WHEN school_name < 'n' THEN 'A-M'
                        WHEN school_name >= 'n' THEN 'N-Z'
                        ELSE NULL END AS school_name_group,
                    COUNT(1) AS players
            FROM benn.college_football_players
            GROUP BY 1;
