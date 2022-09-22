# RPA Customer Segmentation

The marketing department of Reputable Product Agency (RPA) is looking to segment the company users by a number of different criteria.

In this context, a segment is a subset of users that meet different conditions. Segments are used to send marketing campaigns to users who meet specific criteria or to measure the performance of specific marketing campaigns.

Use SQL queries to generate `user` lists for the marketing department. The users dataset is imported into the workspace.

The schema of the table is available [here](https://content.codecademy.com/courses/sql-queries-user-segmentation/users.png).

## Solutions

```
-- 1. What are the column names?
SELECT *
FROM users;

-- Columns: id, email, campaign, test, created_at, birthday
 
-- 2. Find the email addresses and birthdays of users whose birthday is between 1980-01-01 and 1989-12-31, order by birthday ascendingly.
SELECT email, birthday
FROM users
WHERE birthday BETWEEN '1980-01-01' AND '1989-12-31'
ORDER BY birthday ASC;

   
-- 3. Find the emails and creation date of users whose created_at date is prior to May 2017.
SELECT email, created_at
FROM users
WHERE created_at < '2017-05-01'
ORDER BY created_at DESC;


-- 4. Find the emails of the users who received the ‘bears’ test.
SELECT email
FROM users
WHERE test = 'bears';

-- 5. Find all the emails of all users who received a campaign on website BBB.
SELECT email
FROM users
WHERE campaign = 'BBB%';

-- 6. Find all the emails of all users who received ad copy 2 in their campaign.
SELECT email
FROM users
WHERE campaign = '%-2';

-- 7. Find the emails for all users who received both a campaign and a test. 
-- These users will have non-empty entries in the campaign and test columns.
SELECT email
FROM users
WHERE campaign IS NOT NULL
  AND test IS NOT NULL;

-- 8.
-- Challenge
-- One of the members of the marketing team had an idea of calculating how old users were when they signed up.
SELECT 
  id, 
  email, 
  birthday,
  (created_at - birthday) AS age
FROM users
LIMIT 10;
```
