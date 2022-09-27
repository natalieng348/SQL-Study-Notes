#  Cryptocurrency Exchange

Fiddy Cent is a digital currency exchange headquartered in Neo Tokyo. They broker exchanges of Bitcoin, Bitcoin Cash, Ethereum, and Litecoin with fiat currencies in around 50 countries.

Help them analyze their January ledger data using SQL aggregate functions! You are given the transactions table, which contains  both money-in and money-out transactions.

## Solutions

```
-- 1. Let’s start by checking out the whole transactions table:
SELECT * FROM transactions;

-- Columns: id, user_id, date, currency, money_in,	money_out

-- 2. The money_in column records the amount (in USD) the user bought. What is the total money_in in the table?
SELECT SUM(money_in) AS total_money_in
FROM transactions;
-- Total: 17173.0

-- 3. The money_out column records the amount (in USD) the user sold. What is the total money_out in the table?
SELECT SUM(money_out) AS total_money_out
FROM transactions;
-- Total: 33417.

-- 4. It was reported that Bitcoin dominates Fiddy Cent’s exchange. Let’s see if it is true within these dates by answering two questions:

-- How many money_in transactions are in this table?
SELECT COUNT(money_in) AS money_in_count
FROM transactions; 
-- Result: 43

-- How many money_in transactions are in this table where ‘BIT’ is the currency?
SELECT COUNT(money_in) AS money_in_count
FROM transactions
WHERE currency = 'BIT'; 
-- Result: 21

-- 5. What was the largest transaction in this whole table? Was it money_in or money_out?
SELECT MAX(money_in) AS max_money_in
FROM transactions;
-- Result: 6000.0

SELECT MAX(money_out) AS max_money_out
FROM transactions;
-- Result: 15047.0
-- The largest transaction is money_out

-- 6. What is the average money_in in the table for the currency Ethereum (‘ETH’)?
SELECT AVG(money_in) as avg_money_in_eth
FROM transactions
WHERE currency = 'ETH';
-- Result: 131.888888888889

-- 7. Let’s build a ledger for the different dates.
-- Select date, average money_in, and average money_out from the table and group everything by date.
SELECT
  date, 
  ROUND(AVG(money_in),2) AS avg_money_in,
  ROUND(AVG(money_out),2) AS avg_money_out
FROM transactions
GROUP BY date;
```
