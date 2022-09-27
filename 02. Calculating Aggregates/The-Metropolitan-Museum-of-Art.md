The Metropolitan Museum of Art

![SiWlHHW](https://user-images.githubusercontent.com/96028654/192216409-ba3872a0-8c50-408b-ba67-a87adc51d108.jpg)

[The Metropolitan Museum of Art](https://www.metmuseum.org/) of New York is one of the world’s largest and finest art museums.

In this project, you will be working with a table named met that contains the museum’s collection of American Decorative Arts.

It has the following columns:

* id - the id of the art piece
* department - the department of the art piece
* category - the category of the art piece
* title - the title name of the art piece
* artist - the name of the artist
* date - the date(s) of the art piece
* medium - the medium of the art piece
* country - the country of the artist

This data was kindly made publicly available under the [Open Access Policy](https://www.metmuseum.org/about-the-met/policies-and-documents/image-resources).

## Solutions

```
-- 1. Start by getting a feel for the met table:
 SELECT *
 FROM met
 LIMIT 10;

-- 2. How many pieces are in the American Decorative Art collection?
SELECT COUNT(*)
FROM met;

-- 3. Count the number of pieces where the category includes ‘celery’
SELECT COUNT(*)
FROM met
WHERE category LIKE '%celery%';

-- 4. Find the title and medium of the oldest piece(s) in the collection
SELECT
  title,
  medium,
  MIN(date) AS date
FROM met;

-- The result is 1600-1700. Now let's try this:
SELECT 
  title,
  medium,
  date
FROM met
WHERE date LIKE "%1600%";

-- Betty Lamp, Candlestick, and Casement Window are among the oldest pieces in the collection.

-- 5. Find the top 10 countries with the most pieces in the collection.
SELECT
  country,
  COUNT(*) AS pieces_count
FROM met
GROUP BY country
ORDER BY pieces_count DESC
LIMIT 10;

-- 6. There are all kinds of American decorative art in the Met’s collection. Find the categories HAVING more than 100 pieces.
SELECT
  category,
  COUNT(*) AS pieces_count
FROM met
GROUP BY category
HAVING pieces_count > 100
ORDER BY pieces_count DESC;

-- 7. Lastly, let’s look at some bling! Count the number of pieces where the medium contains ‘gold’ or ‘silver’, and sort in descending order.
SELECT
  medium,
  COUNT(*) AS pieces_count
FROM met
WHERE medium LIKE '%gold%' 
  OR medium LIKE '%silver%'
GROUP BY medium
ORDER BY pieces_count DESC;

-- To be more accurate, we can also do the following:
SELECT CASE
  WHEN medium LIKE '%gold%' THEN 'Gold'
  WHEN medium LIKE '%silver%' THEN 'Silver'
  Else NULL
  END AS 'Bling',
  COUNT(*) AS pieces_count
FROM met
GROUP BY Bling
ORDER BY pieces_count DESC;
```
