# Data Warehouse Architecture
-   Kimball's Bus Architecture
-   Independent Data Marts
-   Inmon's Corporate Information Factory (CIF)
-   Hybrid Bus & CIF
 
 ## OLAP Cubes
 -  An OLAP cube is an aggregation of a fact metric on a number of dimensions, eg Movie, Branch, Month.
 -  Easy to communicate to business users
 -  Common OLAP Operations include: Rollup, drill-down, slice, & dice.

 ## OLAP Cubes Operations: Roll-up & Drill Down
 -  Roll-up: Includes going through one dimension like for example the branch, group all of the city and sum them. Sum up the sales of each city by country: e.g US, France (less columns in branch dimension)
 -  Drill-Down: Decompose the sales of each city into smaller districts(more columns in branch dimension)
 -  The OLAP cubes should store the finest grain of data (atomic data), in case we need to drill-down to the lower level, e.g Country -> City -> District -> Street, etc.
