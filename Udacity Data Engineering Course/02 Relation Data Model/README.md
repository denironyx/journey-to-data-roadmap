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
Is the process of trying to improve the read performance of a database at the expense of losing some write performance by adding redundant copies of data.