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