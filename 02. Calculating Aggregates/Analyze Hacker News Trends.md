# Analyze Hacker News Trends

![image](https://user-images.githubusercontent.com/96028654/192205818-c4a366e2-87e9-498f-ab43-cd1ab5612ac4.png)

[Hacker News](https://news.ycombinator.com/) is a popular website run by Y Combinator. It’s widely known by people in the tech industry as a community site for sharing news, showing off projects, asking questions, among other things.

In this project, you will be working with a table named `hacker_news` that contains stories from Hacker News since its launch in 2007. It has the following columns:

* `title`: the title of the story
* `user`: the user who submitted the story
* `score`: the score of the story
* `timestamp`: the time of the story
* `url`: the link of the story

This data was kindly made publicly available under the MIT license.

Let’s get started!

## Solutions

1. Start by getting a feel for the hacker_news table!
Let’s find the most popular Hacker News stories. What are the top five stories with the highest scores?

```
SELECT title, score
FROM hacker_news
ORDER BY score DESC
LIMIT 5;
```

![image](https://user-images.githubusercontent.com/96028654/192206833-812f9c17-fd4a-41f7-9fcd-c668dd94300e.png)

### Hacker News Moderating

2. Recent studies have found that online forums tend to be dominated by a small percentage of their users (1-9-90 Rule). Is this true of Hacker News?
Is a small percentage of Hacker News submitters taking the majority of the points?
First, find the total score of all the stories.

```
SELECT SUM(score) AS total_score
FROM hacker_news;
```

![image](https://user-images.githubusercontent.com/96028654/192207009-0e6bd211-5ac7-4286-a552-c1ce0a07eca5.png)

3. Next, we need to pinpoint the users who have accumulated a lot of points across their stories. Find the individual users who have gotten combined scores of more than 200, and their combined scores.

```
SELECT 
  user,
  SUM(score) AS individual_score
FROM hacker_news
GROUP BY user
HAVING individual_score > 200
ORDER BY individual_score DESC;
```

![image](https://user-images.githubusercontent.com/96028654/192207102-bdf344d2-f13c-4e6b-a989-316874274a73.png)

4. Then, we want to add these users’ scores together and divide by the total to get the percentage.
Add their scores together and divide it by the total sum. So, is Hacker News dominated by these users?

```
SELECT (517 + 309 + 304 + 282) / 6366.0;
```
![image](https://user-images.githubusercontent.com/96028654/192207769-3a0862b9-0f98-459f-9249-b607991743ed.png)

That is ≈ 22%. These 4 users have a combined 22% of the total scores in the table. Jeez!

5. Oh no! While we are looking at the power users, some users are rickrolling — tricking readers into clicking on a link to a funny video and claiming that it links to information about coding. The url of the video is: https://www.youtube.com/watch?v=dQw4w9WgXcQ. How many times has each offending user posted this link?

```
SELECT 
  user,
  COUNT(*) AS rickroll_count
FROM hacker_news
WHERE url = 'https://www.youtube.com/watch?v=dQw4w9WgXcQ'
GROUP BY user
ORDER BY rickroll_count DESC;
```

![image](https://user-images.githubusercontent.com/96028654/192208210-6c008c19-98f2-4ab7-9ab0-655cc1539a2a.png)

6. Hacker News stories are essentially links that take users to other websites.
Which of these sites feed Hacker News the most: GitHub, Medium, or New York Times?
First, we want to categorize each story based on their source.

```
SELECT CASE
  WHEN url LIKE '%github.com%' THEN 'GitHub'
  WHEN url LIKE '%medium.com%' THEN 'Medium'
  WHEN url LIKE '%nytimes.com%' THEN 'NY Times'
  ElSE 'Other'
  END AS 'source'
FROM hacker_news;
```


7. Next, build on the previous query:
Add a column for the number of stories from each URL using COUNT().
Also, GROUP BY the CASE statement.
Remember that you can refer to a column in GROUP BY using a number.

```
SELECT CASE
  WHEN url LIKE '%github.com%' THEN 'GitHub'
  WHEN url LIKE '%medium.com%' THEN 'Medium'
  WHEN url LIKE '%nytimes.com%' THEN 'NY Times'
  ElSE 'Other'
  END AS 'source',
  COUNT(*) AS stories_count
FROM hacker_news
GROUP BY source;
```

![image](https://user-images.githubusercontent.com/96028654/192209062-afa44d91-a986-4edb-8368-81af92cd431e.png)

8. Every submitter wants their story to get a high score so that the story makes it to the front page, but…
What’s the best time of the day to post a story on Hacker News?

```
SELECT 
  MAX(score) AS highest_score,
  timestamp
FROM hacker_news;
```

![image](https://user-images.githubusercontent.com/96028654/192209680-cfabc91c-3a16-4c4c-a58a-3c50dd3b88d2.png)

9. SQLite comes with a strftime() function - a very powerful function that allows you to return a formatted date. It takes two arguments: `strftime(format, column)`. Let’s test this function out:

```
SELECT timestamp,
  strftime('%H', timestamp)
FROM hacker_news
GROUP BY timestamp
LIMIT 20;
```

![image](https://user-images.githubusercontent.com/96028654/192210049-ac1789e2-a0c3-4fe0-ac9a-85dd4c4e3f28.png)


10. Okay, now we understand how strftime() works. Let’s write a query that returns three columns:
* The hours of the `timestamp`
* The average `score` for each hour
* The _count_ of stories for each hour

```
SELECT 
  strftime('%H', timestamp) AS hour,
  AVG(score) AS avg_score,
  COUNT(*) AS stories_count
FROM hacker_news
GROUP BY hour;
```

![image](https://user-images.githubusercontent.com/96028654/192210532-211f09c8-9d41-4479-a030-a78af097ab7a.png)

11. Let’s edit a few things in the previous query:
Round the average scores `(ROUND())`. Rename the columns to make it more readable `(AS)`.
Add a `WHERE` clause to filter out the `NULL` values in `timestamp`.
Take a look at the result again: What are the best hours to post a story on Hacker News?

```
SELECT 
  strftime('%H', timestamp) AS hour,
  ROUND(AVG(score)) AS avg_score,
  COUNT(*) AS stories_count
FROM hacker_news
WHERE hour IS NOT NULL
GROUP BY hour
ORDER BY avg_score DESC;
```
The best hours to post are in the morning around 7 am and afternoon around 6 - 8 pm!

![image](https://user-images.githubusercontent.com/96028654/192211276-fa7c5b2e-725a-4dab-98fe-5ba8d840d419.png)
