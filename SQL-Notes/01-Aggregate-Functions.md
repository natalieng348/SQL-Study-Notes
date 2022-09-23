# SQL Notes

This is my notes for Codecademy 'Analyze Data with SQL' Course.

## Aggregate Functions

### Basic aggregate functions

* `COUNT()`: count the number of rows
* `SUM()`: the sum of the values in a column
* `MAX()`/`MIN()`: the largest/smallest value
* `AVG()`: the average of the values in a column
* `ROUND()`: round the values in the column

### `HAVING`

* `HAVING` limit the results of a query based on an aggregate property

* `HAVING` always come after `GROUP BY`, but before `ORDER BY` and `LIMIT`.

* Difference between `HAVING` and `WHERE`:
    * `HAVING` filters by **group** while `WHERE` filters by individual rows.
    
* Almost all `WHERE` functions can be done by `HAVING`.
