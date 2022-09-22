# Davie's Burgers Subway Ad

![image](https://user-images.githubusercontent.com/96028654/191636606-f672e4ef-c452-4650-8382-0df84e604542.png)


Do you remember **Davie’s Burgers** from our Learn CSS course? Well, the restaurant business has been booming and it is now looking to place a catchy advertisement in the local subway station.

Help them dig into their orders table to see if there is anything interesting in there for a funny tagline!

## Solutions

```
-- 1. What are the column names?
SELECT *
FROM orders;
-- 6 COLUMNS: id, user_id, order_date, restaurant_id, item_name, special_instructions

-- 2. How recent is this data?
-- Use DISTINCT to find out all the unique order_date values in this table.
SELECT DISTINCT order_date
FROM orders
ORDER BY order_date DESC;
-- Latest order date is 2017-06-30

-- 3. Instead of selecting all the columns using *, write a query that selects only the special_instructions column. 
-- Limit the result to 20 rows.
SELECT special_instructions
FROM orders
LIMIT 20;

-- 4. Can you edit the query so that we are only returning the special instructions that are not empty?
SELECT special_instructions
FROM orders
WHERE special_instructions IS NOT NULL;

-- 5. Let’s go even further and sort the instructions in alphabetical order (A-Z).
SELECT special_instructions
FROM orders
WHERE special_instructions IS NOT NULL
ORDER BY special_instructions ASC;

-- 6. Let’s search for special instructions that have the word ‘sauce’. Are there any funny or interesting ones? 
SELECT special_instructions
FROM orders
WHERE special_instructions LIKE '%sauce%';

-- 7. Let’s search for special instructions that have the word ‘door’. Any funny or interesting ones?
SELECT special_instructions
FROM orders
WHERE special_instructions LIKE '%door%';

-- 8. Let’s search for special instructions that have the word ‘box’. Any funny or interesting ones?
SELECT special_instructions
FROM orders
WHERE special_instructions LIKE '%box%';

-- 9. Instead of just returning the special instructions, also return their order ids. For more readability:
-- Rename id as ‘#’
-- Rename special_instructions as ‘Notes’
SELECT 
  id AS '#',
  special_instructions AS 'Notes'
FROM orders
WHERE special_instructions LIKE '%box%';

-- 10
-- Challenge
-- They have asked you to query the customer who made the phrase 'Draw a narwhal on the delivery box.'. 
-- Return the item_name restaurant_id, and user_id for the person created the phrase.
SELECT
  user_id,
  item_name,
  restaurant_id
FROM orders
WHERE special_instructions = 'Draw a narwhal on the delivery box.';
```
