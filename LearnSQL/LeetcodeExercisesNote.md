# Leetcode Exercises Note

### TODO
178. Rank Scores
180. Consecutive Numbers
196. Delete Duplicate Emails
627. Swap Salary
626. Exchange Seats

### LIMIT and OFFSET

        LIMIT 1 OFFSET 1        

* OFFSET: Skip n rows from top
* LIMIT: Show only n rows from top

### GROUP BY and HAVING
* Remember to use HAVING to set conditions along with GROUP BY.

### JOINs
* To get data from only set1

        SELECT *
        FROM table1
        LEFT JOIN table2
        ON table1.key = table2.key
        WHERE table2.key IS NULL;
