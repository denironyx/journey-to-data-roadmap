## Relational Data Model

### Databases

### Importance of Relational Databases

### OLAP VS OLTP
Online Analytical Processing (OLAP):
    Databases optimized for these workloads allow for complex analytical and ad hoc queries. These type of databases are optimized for reads. OLAP queries can tell you how many shoes that was sold last week in California.

Online Transactional Processing (OLTP):
    Databases optimized for these workloads allow for less complex queries in large volume. The types of queries for these databases are read, insert, update, and delete. OLTP will tell you the price of the shoe. It has little or no aggregation.

### Structuring the Database Normalization
-   Normalization: To reduce data redundancy(remove duplicate) and increase data integrity(data gotten will be the exact data).
-   Denorminalization: Must be done if you are doing read heavy workloads to increase performance. Reducing the number of copies of the data and increasing the likely hood that the data is correct in all location

Normalization: This is the process of structuing a relational database in accordance with a series of normal forms in order to reduce data redundancy and increase data integrity.

Objectives of Normal Form
1. To free the database from unwanted insertions, updates, and deletion dependencies.
2. To reduce the need for refactoring the database as new types of data are introduced.
3. To make the relational model more informative to users
4. To make the database neutral to the query statistics.

### Normal Forms
The process of normalization is a step by step process. 
-   First Normal Form (1NF)
-   Second Normal Form (2NF)
-   Third Normal Form (3NF)
There are about siz normal forms but most database try to achieve up to the 3NF. The 4-6NF is pretty much for academic purpose and not for production. 

### 1 NF
How to reach 1st Normal form
-   Atomic values: each cell contains unique and single values.
-   Be able to add data without altering the table.
-   Separate different relations into different tables.
-   Keep relationships between tables together with foreign keys.

### 2 NF
How to reach 2nd Normal Form
-   Have reached 1NF
-   All columns in the table must rely on the Primary Key.

### 3 NF
How to reach 3rd Normal Form
-   Must be in 2nd Normal Form
-   No transitive dependencies

## Denormalization
This is the process of trying to improve the read performance of a databaase at the expense of losing some write performance by adding redundant copies of data.ical

### Logical Design Change
1.  The Designer is incharge of keeping data consistent
2.  Reads will be faster(select)
3.  Writes will be slower (insert, update, delete)

## Denormalization vs Normalization
** Normalization** is about trying to increase data integrity by reducing the number of copies of the data. Data that needs to be added or updated will be done in as few places as possible.

** Denormalization** is trying to increase performance by reducing the number of joins between tables (as joins can be slow). Data integrity will take a bit of a potential hit, as there will be more copies of the data (to reduce JOINS).

### Facts and Dimension Tables
-   Work together to create an organized adta models
-   While fact and dimension are not created differently in the DDL, they are conceptual and extremely important for organization.

**Fact table** consists of the measurements, metrics or facts of a business process.

**Dimension table** is a structure that categorizes facts and measures in order to enable users to answer business questions. Dimensions are people, products, place, and time.

### Implementing Different Schemas
Two of the most popular data mart schema for datawarehouses are:
1.  Star Schema
2.  Snowflake Schema

### Star Schema
Star schema is the simplest style of data mart schema. The star schema consists of one of more fact tables referenciing any number of dimension tables.

#### Why "star" schema?
-   Gets its name from the physical model resembling a star shape.
-   A fact table is at its center.
-   Dimension table surrounds the fact table representing the star's points.

Benefits  
-   Allows Denormalization
-   Simplifies queries
-   Fast aggregation

Drawbacks
-   Issues that come with denormilization
-   Data integrity
-   Decrease query flexibility
-   Many to many relationship

### Snowflake Schema
It's the logical arrangement of tables in a multidimensional database represented by centralized fact tables which are connected to multiple dimensions.

#### Why "snowflake" schema?
It's a complex snowflake shape that emerges when the dimensions of a snowflake schema are elaborated, having multiple levels of relationships, child tables having multiple parents.

### Snowflake vs Star
-   Star schema is a special, simplified case of the snowflake schema.
-   Star schema does not allow for one to many relationships while the snowflake schema does.
-   Snowflake schema is more normalized than Star schema but only in 1NF or 2NF