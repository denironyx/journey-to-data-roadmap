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

## OLAP Cubes Operations: Slice
-   Reducing N dimensions to N-1 dimensions by restricting one dimension to a single value. E.g month='MAR'

## OLAP Cubes Operations: Dice
-   Same dimensions but computing a sub-cube by restricting, some of the values of the dimensions
-   E.g. Month in ['FEB', 'MAR'] and movie in ['Avatar', 'Batman'] branch = 'NY'

### OLAP Cubes query optimization
-   Business users will typically want to slice, dice, rollup and drill-down all the time.
-   Each such combination will potentially go through all the facts table (suboptimal)
-   The "GROUP by CUBE (movie, branch, month)" will make one pass through the facts table and will aggregate all possible combinations of groupings, of length 0,1,2 and 3 e.g:
    -   Total Revenue
        - Revenue by movie, Revenue by movie, branch 
        - Revenue by branch, Revenue by branch, month
        - Revenue by month, Revenue by movie, month
-   Saving/Materializing the output of the CUBE operation and using it is usually enough to answer all forthcoming aggregation from business users without having to process the whole facts table again.