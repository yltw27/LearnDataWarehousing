# Data Modeling

* Definition: Data modeling is the process of creating a data model for the data to be stored in a database. This data model is a conceptual representation of
    - Data objects
    - The associations between different data objects
    - The rules

### OLAP, Online Analytical Processing
* OLAP is a category of software that allows users to analyze information from multiple database systems at the same time
* OLAP Cube (or hypercube): a data structure optimized for very quick data analysis. The cube can store and analyze **multidimensional** data in a logical and orderly manner
* 4 Basic analytical operations of OLAP:
    1. Roll-up (also called consolidation or aggregation)
        - In the roll-up process at least one or more dimensions need to be removed. E.g. Combine multiple columns as a new column
    2. Drill-down
        - In drill-down data is fragmented into smaller parts
    3. Slice
        - Select one or more specific dimensions and create a new sub-cube
    4. Pivot
        - Rotate the data axes to provide a substitute presentation of data

### OLTP, Online Transaction Processing
* OLTP supports transaction-oriented applications in a 3-tier architecture. OLTP administers day to day transaction of an organization.
* Examples: ATM center (OLTP system makes sure that withdrawn amount will be never more than the amount present in the bank)

### Differences between OLAP and OLTP
* The primary objective of OLAP is data analysis and not data processing, but the primary objective ot OLTP is data processing and not data analysis
* OLAP
    * Benefits
        - The main benefit of OLAP is the consistency of information and calculations
        - Creates a single platform for all type of business analytical needs which includes planning, budgeting, forecasting, and analysis
        - Easily apply security restrictions on users and objects to comply with regulations and protect sensitive data
    * Drawbacks
        - Implementation and maintenance are dependent on IT professional because the traditional OLAP tools require a complicated modeling procedure
        - OLAP tools need cooperation between people of various departments to be effective which might always be not possible
* OLTP
    * Benefits
        - It administers daily transactions of an organization
        - OLTP widens the customer base of an organization by simplifying individual processes
    * Drawbacks
        - If OLTP system faces hardware failures, then online transactions get severely affected
        - OLTP systems allow multiple users to access and change the same data at the same time which many times created unprecedented situation

* More [https://www.guru99.com/oltp-vs-olap.html](https://www.guru99.com/oltp-vs-olap.html)