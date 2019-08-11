# Data Warehouse

* Definition
    * Data Wareshouse 是一個以分析為目的而做各種資料集成的系統
    * A modern business typically have data stored in different places (data sources). This can be data from:
        - Application databases
        - Web applications
        - Spreadsheets
    * A data warehouse sync data from different sources into a single place for all data reporting needs
    * It provides data that can be trusted to be reliable, and can handle the querying workload from all employees in the company.
    * You design and build your data warehouse based on your reporting requirements. After you identified the data you need, you design the data to flow information into your data warehouse.    

* Design a Data Warehouse
    1. Create a schema for each data source
        * Quickly identify the data source that each table comes from, which helps as your number of data sources grow
        * Help you assign specific permissions (read/write) for each data source
    2. Sync source data into your data warehouse
        * Design the ETL script with these considerations:
            1. Do not include unnecessary columns
            2. Rename column names to make them more descriptive or database friendly
            3. Filter out obviously unnecessary records
            4. Map record values to make them more readable (instead of abbreviated names)
            5. Apply database indexes to your destination table after the import is done
            6. Error Handling: Setup emails/Slack alert message to be sent to the relevant stakeholders (especially data analysts) with detailed error logs when the job fails. You may want to setup automated retry attempts (or automated recovery processes) within a specific time period to reduce the number of false positives in this case
    3. Transform your raw/source data (You might not need this step at first)
    4. Transform data to solve a specific problem
        * Data transforms should be created only to address a practical use case or problem from your reporting
        * It's important to write efficient SQL commands to reduce the time producing each report
    5. Create your internal data documents
        * Tables and columns in your source data, and how to interpret them
        * Include data diagram if any
        * How to read your columns in your reports (dashboard, metrics) and any underlying assumptions behind them

* 2 ways to load data into the analytics database
    1. ETL: Extract, transform and load. This is the way to generate our **data warehouse**. First, extract the data from the production database, transform the data according to our requirement, and then, load the data into our data warehouse
    2. ELT: Extract, load and transform. First, extract the data from the production database, load it into the database and then transform the data. This way is called **Data Lake** and it’s a new concept to manage our big data
