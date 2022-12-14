# RPA Fraud Detection

Reputable Product Agency (RPA) has started receiving complaints from their credit card processor about fraudulent transactions. Help your finance department identify potentially risky transactions before they finish processing.

This dataset contains a single table, transaction_data.

The schema of this table is available [here](https://content.codecademy.com/courses/sql-queries-fraud/transaction-data.png).


## Solutions 

```
-- 1
-- What are the column names?
SELECT *
FROM transaction_data
LIMIT 10;

-- Columns: id, full_name, email, zip, ip_address

-- 2
-- Find the full_names and emails
-- of the transactions listing 20252 as the zip code.
SELECT full_name, email
FROM transaction_data
WHERE zip = '20252';

-- 3
-- Use a query to find the names 
-- and emails associated with these transactions.
SELECT full_name, email
FROM transaction_data
WHERE full_name = 'Art Vandelay'
  OR full_name LIKE '% der %';

-- 4
-- There are some irregularities in the IP addresses starting with '10.'
-- Find the ip_addresses and emails listed with these transactions.
SELECT ip_address, email
FROM transaction_data
WHERE ip_address LIKE '10.%';

-- 5
-- Find the emails in transaction_data with
-- ‘temp_email.com’ as a domain.
SELECT email
FROM transaction_data
WHERE email LIKE '%temp_email.com';

-- 6
-- Find the transaction occurred from an IP address starting with ‘120.’ and full name starts with ‘John’.
SELECT *
FROM transaction_data
WHERE ip_address LIKE '120.%'
  AND full_name LIKE 'John%';

-- 7
-- Challenge
-- Return only those customers residing in GA. Use the list of ZIP CODE prefixes
-- (https://en.wikipedia.org/wiki/List_of_ZIP_Code_prefixes)
-- to determine the best query for zip codes belonging to Georgia(GA).
SELECT *
FROM transaction_data
WHERE zip LIKE '30%'
  OR zip LIKE '31%';
```
