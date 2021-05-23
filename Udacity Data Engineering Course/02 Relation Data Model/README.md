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

In this example, it helps to think about the Dimension tables providing the following information:
    • Where the product was bought? (Dim_Store table)
    • When the product was bought? (Dim_Date table)
    • What product was bought? (Dim_Product table)
The Fact table provides the metric of the business process (here Sales).
    • How many units of products were bought? (Fact_Sales table)

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

If you are familiar with Entity Relationship Diagrams (ERD), you will find the depiction of STAR and SNOWFLAKE schemas in the demo familiar. The ERDs show the data model in a concise way that is also easy to interpret. ERDs can be used for any data model, and are not confined to STAR or SNOWFLAKE schemas. Commonly available tools can be used to generate ERDs. However, more important than creating an ERD is to learn more about the data through conversations with the data team so as a data engineer you have a strong understanding of the data you are working with.
More information about ER diagrams can be found at this Wikipedia page.

### Data Definition and Constraints
The CREATE statement in SQL has a few important constraints that are highlighted below.
NOT NULL
The NOT NULL constraint indicates that the column cannot contain a null value.
Here is the syntax for adding a NOT NULL constraint to the CREATE statement:
```CREATE TABLE IF NOT EXISTS customer_transactions (
    customer_id int NOT NULL, 
    store_id int, 
    spent numeric
);```

You can add NOT NULL constraints to more than one column. Usually this occurs when you have a COMPOSITE KEY, which will be discussed further below.
Here is the syntax for it:
```CREATE TABLE IF NOT EXISTS customer_transactions (
    customer_id int NOT NULL, 
    store_id int NOT NULL, 
    spent numeric
);```
UNIQUE
The UNIQUE constraint is used to specify that the data across all the rows in one column are unique within the table. The UNIQUE constraint can also be used for multiple columns, so that the combination of the values across those columns will be unique within the table. In this latter case, the values within 1 column do not need to be unique.

Let's look at an example.
```CREATE TABLE IF NOT EXISTS customer_transactions (
    customer_id int NOT NULL UNIQUE, 
    store_id int NOT NULL UNIQUE, 
    spent numeric 
);```
Another way to write a UNIQUE constraint is to add a table constraint using commas to separate the columns.
```CREATE TABLE IF NOT EXISTS customer_transactions (
    customer_id int NOT NULL, 
    store_id int NOT NULL, 
    spent numeric,
    UNIQUE (customer_id, store_id, spent)
);```
PRIMARY KEY
The PRIMARY KEY constraint is defined on a single column, and every table should contain a primary key. The values in this column uniquely identify the rows in the table. If a group of columns are defined as a primary key, they are called a composite key. That means the combination of values in these columns will uniquely identify the rows in the table. By default, the PRIMARY KEY constraint has the unique and not null constraint built into it.

Let's look at the following example:
```CREATE TABLE IF NOT EXISTS store (
    store_id int PRIMARY KEY, 
    store_location_city text,
    store_location_state text
);```
Here is an example for a group of columns serving as composite key.
```CREATE TABLE IF NOT EXISTS customer_transactions (
    customer_id int, 
    store_id int, 
    spent numeric,
    PRIMARY KEY (customer_id, store_id)
);```
To read more about these constraints, check out the PostgreSQL documentation.


### Upsert
In RDBMS language, the term upsert refers to the idea of inserting a new row in an existing table, or updating the row if it already exists in the table. The action of updating or inserting has been described as "upsert".
The way this is handled in PostgreSQL is by using the INSERT statement in combination with the ON CONFLICT clause.

### INSERT
The INSERT statement adds in new rows within the table. The values associated with specific target columns can be added in any order.
Let's look at a simple example. We will use a customer address table as an example, which is defined with the following CREATE statement:
```CREATE TABLE IF NOT EXISTS customer_address (
    customer_id int PRIMARY KEY, 
    customer_street varchar NOT NULL,
    customer_city text NOT NULL,
    customer_state text NOT NULL
);
Let's try to insert data into it by adding a new row:
INSERT into customer_address (
VALUES
    (432, '758 Main Street', 'Chicago', 'IL'
);
Now let's assume that the customer moved and we need to update the customer's address. However we do not want to add a new customer id. In other words, if there is any conflict on the customer_id, we do not want that to change.
This would be a good candidate for using the ON CONFLICT DO NOTHING clause.
INSERT INTO customer_address (customer_id, customer_street, customer_city, customer_state)
VALUES
 (
 432, '923 Knox Street', 'Albany', 'NY'
 ) 
ON CONFLICT (customer_id) 
DO NOTHING;
Now, let's imagine we want to add more details in the existing address for an existing customer. This would be a good candidate for using the ON CONFLICT DO UPDATE clause.
INSERT INTO customer_address (customer_id, customer_street)
VALUES
    (
    432, '923 Knox Street, Suite 1' 
) 
ON CONFLICT (customer_id) 
DO UPDATE
    SET customer_street  = EXCLUDED.customer_street;
We recommend checking out these two links to learn other ways to insert data into the tables.
    • PostgreSQL tutorial
    • PostgreSQL documentation

What we learned:
    • What makes a database a relational database and Codd’s 12 rules of relational database design
    • The difference between different types of workloads for databases OLAP and OLTP
    • The process of database normalization and the normal forms.
    • Denormalization and when it should be used.
    • Fact vs dimension tables as a concept and how to apply that to our data modeling
    • How the star and snowflake schemas use the concepts of fact and dimension tables to make getting value out of the data easier.
