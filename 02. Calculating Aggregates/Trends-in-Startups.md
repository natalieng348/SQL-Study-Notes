# Trends in Startups

Howdy! It’s your first day as a TechCrunch reporter. 
Your first task is to write an article on the rising trends in the startup world.

To get you started with your research, your boss emailed you a **project.sqlite** file that contains a table called `startups`.

It is a portfolio of some of the biggest names in the industry.

Write queries with aggregate functions to retrieve some interesting insights about these companies.


## Solutions

```
-- 1. Getting started, take a look at the startups table:
SELECT *
FROM startups;
-- Result: 10 Columns - name, location, category, employees, raised, valuation, founded, stage, ceo, info

-- 2. Calculate the total number of companies in the table.
SELECT COUNT(name) AS total_company_count
FROM startups;
-- Result: 70

-- 3. Calculate the total value of all companies in this table.
SELECT SUM(valuation) AS total_value
FROM startups;
-- Result: 974,455,790,000

-- 4. What is the highest amount raised by a startup?
SELECT MAX(raised) AS highest_raised
FROM startups;
-- Result: 11,500,000,000

-- 5. Returns the maximum amount of money raised, during ‘Seed’ stage.
SELECT MAX(raised) AS seed_max_raised
FROM startups
WHERE stage = 'Seed';

-- 6. In what year was the oldest company on the list founded?
SELECT MIN(founded) AS earliest_founded
FROM startups;

-- Let's find out the valuations among different sectors:

-- 7. Return the average valuation.
SELECT AVG(valuation)
FROM startups;

-- 8. Return the average valuation, in each category.
SELECT 
  category,
  AVG(valuation) AS avg_valuation
FROM startups
GROUP BY category;

-- 9. Return the average valuation, in each category.
-- Round the averages to two decimal places.
SELECT
  category,
  ROUND(AVG(valuation), 2) AS avg_valuation
FROM startups
GROUP BY category;

-- 10. Return the average valuation, in each category.
-- Round the averages to two decimal places.
-- Lastly, order the list from highest averages to lowest.
SELECT
  category,
  ROUND(AVG(valuation), 2) AS avg_valuation
FROM startups
GROUP BY category
ORDER BY avg_valuation DESC;
 
-- What are the most competitive markets?

-- 11. Return the name of each category with the total number of companies that belong to it.
SELECT
  category,
  COUNT(*) AS company_count
FROM startups
GROUP BY category;

-- 12. Filter the result to only include categories that have more than three companies in them.
SELECT
  category,
  COUNT(*) AS company_count
FROM startups
GROUP BY category
HAVING company_count > 3
ORDER BY company_count DESC;

-- 13. What is the average size of a startup in each location?
SELECT
  location,
  AVG(employees) AS avg_size
FROM startups
GROUP BY location;

-- 14. What is the average size of a startup in each location, with average sizes above 500?
SELECT
  location,
  AVG(employees) AS avg_size
FROM startups
GROUP BY location
HAVING avg_size > 500;
```
