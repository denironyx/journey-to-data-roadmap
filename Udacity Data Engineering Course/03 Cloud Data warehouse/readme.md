## What is Data Warehouse
A data warehouse is a copy of transaction data specifically structured for query and analysis - Kimball

A data warehouse is subject-oriented, integrated, nonvolatile, and time-variant collection of data in support of management's decisions. - INMON

A data warehouse is a system that retrieves and consolidates data periodically from the source systems into a dimensional or normalized data store. It usually keeps years of history and is queried for business intelligence or other analytical activities. It is typically updated in batches, not every time a transaction happens in the source systems. - Rainardi

Data Warehouse is a system(including processes, technologies & data representations) that enables us to support analytical processes.

### Operational vs Analytical Business Process

### Operation Processes (make it work):
-   Find goods & make orders (for customers)
-   Stocks and find goods(for inventory staff)
-   Pick up and deliver goods (for delivery staff)
-   Operational Databases, excellent for operations
-   Operational Databases, no redundancy, high integrity.

### Analytical Processes (what is going on?)
-   Assess the performance of sales staff (for HR)
-   See the effect of different sales channesl (for marketing)
-   Monitor sales growth(for management).
-   Operational Databases, too slow for analytics, too many joins
-   Operational Databases, are too hard to understand. Because they are model for data storage.


Data warehouse: Tech Perspective
 
The first thing we expect in the data warehouse is to perform an ETL, that is extract the data from the source systems used for the *operation processes*, transform the data and load it into a dimensonal model.

The dimensional model is designed to a) make it easy for business users to work with the data. b) improve analytical queries performance. The technologies used for storing dimensional models are different than traditional technologies.

Finally, the analytical processes requires the business-user-facing application are needed with clear visuals

### Data warehouse goals
-   Simple to understand
-   Quality assured
-   Performant
-   Handles new questions well
-   Secure

## Dimensional Modelling
### Dimensional Modelling Goals
-   Easy to understand
-   Fast analytical query performance
-   Star Schema - Joins with dimensions only good for OLAP not OLTP
-   3NF - Lots of expensive joins, hard to explain to business users.

## FACTs and Dimensions
Fact tables
-   Record business events, like an order, a phone call, a book reveiew.
-   Fact tables columns record events recorded in quantifiable metrics like quantity of an item, duration of a call, a book rating.

Dimension tables
-   Record the context of the business events, e.g. who, what, where, why, etc.
-   Dimension tables columns contain attributes like the store at which an item is purchased, or the customer who made the call, etc

### Fact or Dimension Dilemma
-   For facts, if you're unsusre if a column is a fact or dimension, the simplest rule is that a fact is usually: *Numeric & Additive*

-   Examples facts:
    -   A comment on an article represent an event but we can not easily make a statistic out of it content per se (not a good fact)
    -   Invoice number is numeric but adding it does not make sense (Not a good fact)
    -   Total amount of an invoice could be added to compute total sales (A good fact)

-   Examples dimensions:
    -   Date and time are always a dimension
    -   Physical locations and their attributes are good candidates dimensions
    -   Human Roles like customers and staff always good candidates for dimensions
    -   Goods sold always good candidates for dimensions.

#### Example: The DVD Rentals Sample Database
-   To master the art of dimensional modelling, one needs to see lots of schemas and think about how to design facts and dimensions from them. 

## Naive ETL: From 3NF to ETL
-   Query the 3NF DB (Extract)
    -   Join tables together(a bit of denormalization)
    -   Changes types
    -   Add new columns
-   Loading (LOAD):
    -   Insert into facts and dimension tables