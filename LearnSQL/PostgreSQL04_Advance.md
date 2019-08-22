# PostgreSQL Advance

### Data Types
* Boolean
    * Use **boolean** or **bool** keyword to declare a column with the Boolean data type.
    * 3 possible values: true, false, null
    * When you insert data into a Boolean column, PostgreSQL converts it to a Boolean value 
        * 1, yes, y, t, true ->  true
        * 0, no, n, f, false ->  false

* Character
    * PostgreSQL provides 3 character data types: 
        1. **CHAR(n)**: The fixed-length character with space padded. If you insert a string that is shorter than the length of the column, PostgreSQL pads spaces. If you insert a string that is longer than the length of the column, PostgreSQL will issue an error.
        2. **VARCHAR(n)**: Variable-length character string. With VARCHAR(n), you can store up to n characters. PostgreSQL does not pad spaces when the stored string is shorter than the length of the column.
        3. **TEXT**: The variable-length character string. Theoretically, text data is a character string with **unlimited** length.

* Numeric
    * PostgreSQL provides2 distinct types of floating-point numbers:
        1. Integers
            * **SMALLINT**: 2-byte signed integer that has a range from -32,768 to 32,767
            * **INT**: a 4-byte integer that has a range from -2,147,483,648 to 2,147,483,647
            * **Serial**: the same as integer except that PostgreSQL will automatically generate and populate values into the SERIAL column.
        2. Floating-point numbers
            * **float(n)**: a floating-point number whose precision, at least, n, up to a maximum of 8 bytes.
            * **real or float8**: a 4-byte floating-point number.
            * **numeric or numeric(p,s)**: a real number with p digits with s number after the decimal point. The numeric(p,s) is the exact number.

* Temporal
    * The temporal data types allow you to store date and /or  time data. PostgreSQL has 5 main temporal data types:
        1. **DATE** stores the dates only
        2. **TIME** stores the time of day values
        3. **TIMESTAMP** stores noth date and time values
        4. **TIMESTAMPTZ** is a timezone-aware timestamp data type
        5. **INTERVAL** stores periods of time

* UUID, Universal Unique Identifiers
    * The UUID values guarantee a better uniqueness than SERIAL and can be used to hide sensitive data exposed to the public such as values of id in URL.

* Array

* JSON
    1. **JSON**: stores plain JSON data that requires reparsing for each processing
    2. **JSONB**: stores JSON data in a binary format which is faster to process but slower to insert. In addition, JSONB supports indexing, which can be an advantage.

* hstore

* Special types
    * box– a rectangular box.
    * line – a set of points.
    * point– a geometric pair of numbers.
    * lseg– a line segment.
    * polygon– a closed geometric.
    * inet– an IP4 address.
    * macaddr– a MAC address.
