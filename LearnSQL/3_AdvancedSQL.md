# Advanced SQL

Based on [Mode: SQL Tutorial](https://mode.com/sql-tutorial/)

### SQL Data Types
* Some basic data types [more](https://www.w3schools.com/sql/sql_datatypes.asp)
![Basic SQL Data Types](attachments/SQLDataTypes.png)

* Use **CAST** or **CONVERT** to change the data type to a numeric one that will allow you to perform the sum. Here are 2 types of syntax:

        SELECT CAST(funding_total_usd AS varchar),
                founded_at_clean::varchar
        FROM tutorial.crunchbase_companies_clean_date;

### SQL Date Format
* Arithmetic operations could be applied on date or time data types. (timestamp show as *0 years 0 mons 503 days 0 hours 0 mins 0.00 secs*)

        SELECT permalink,
                founded_at_clean,
                acquired_at_cleaned - founded_at_clean::timestamp AS time_to_acquisition
        FROM tutorial.crunchbase_companies_clean_date
        WHERE founded_at_clean IS NOT NULL;
        
        SELECT permalink,
                founded_at_clean,
                founded_at_clean::timestamp + INTERVAL '1 week' AS plus_one_week
        FROM tutorial.crunchbase_companies_clean_date
        WHERE founded_at_clean IS NOT NULL;

        SELECT permalink,
                founded_at_clean,
                NOW() - founded_at_clean::timestamp AS founded_time_ago
        FROM tutorial.crunchbase_companies_clean_date
        WHERE founded_at_clean IS NOT NULL;

        SELECT companies.category_code,
                COUNT(CASE WHEN acquisitions.acquired_at_cleaned <= companies.founded_at_clean::timestamp + INTERVAL '3 years' THEN 1 ELSE NULL END) AS acquired_3_yrs,
                COUNT(CASE WHEN acquisitions.acquired_at_cleaned <= companies.founded_at_clean::timestamp + INTERVAL '5 years' THEN 1 ELSE NULL END) AS acquired_5_yrs,
                COUNT(CASE WHEN acquisitions.acquired_at_cleaned <= companies.founded_at_clean::timestamp + INTERVAL '10 years' THEN 1 ELSE NULL END) AS acquired_10_yrs,
                COUNT(1) AS total
        FROM tutorial.crunchbase_companies_clean_date companies
        JOIN tutorial.crunchbase_acquisitions_clean_date acquisitions
        ON acquisitions.company_permalink = companies.permalink
        WHERE founded_at_clean IS NOT NULL
        GROUP BY 1
        ORDER BY 5 DESC;

### Using SQL String Functions to Clean Data
* LEFT, RIGHT and LENGTH
    * You can use LEFT to pull a certain number of characters from the left side of a string and present them as a separate string. RIGHT does the same thing, but from the right side. E.g. Below lines help seperate date and time

            SELECT incidnt_num,
                    date,
                    LEFT(date, 10) AS cleaned_date,
                    RIGHT(date, LENGTH(date) - 11) AS cleaned_time
            FROM tutorial.sf_crime_incidents_2014_01;

    * The innermost functions will be evaluated first.

* TRIM
    * The TRIM function is used to remove characters from the beginning and end of a string. 

            SELECT location,
                    TRIM(both '()' FROM location)
            FROM tutorial.sf_crime_incidents_2014_01;

    * The TRIM function takes 3 arguments. 
        1. Whether you want to remove characters from the beginning (**leading**), the end (**trailing**), or both (**both**, as used above)
        2. All characters to be trimmed. Any characters included in the single quotes will be removed from both beginning, end, or both sides of the string
        3. The text you want to trim using FROM.

* POSITION and STRPOS
    * POSITION allows you to specify a substring, then returns a numerical value equal to the character number (counting from left) where that substring first appears in the target string. 

            SELECT incidnt_num,
                    descript,
                    POSITION('A' IN descript) AS a_position
            FROM tutorial.sf_crime_incidents_2014_01;

    * You can also use the STRPOS function to achieve the same results—just replace IN with a comma and switch the order of the string and substring:

            SELECT incidnt_num,
                    descript,
                    STRPOS(descript, 'A') AS a_position
            FROM tutorial.sf_crime_incidents_2014_01

    * Both the POSITION and STRPOS functions are **case-sensitive**. If you want to look for a character regardless of its case, you can make your entire string a single by using the UPPER or LOWER functions described below.