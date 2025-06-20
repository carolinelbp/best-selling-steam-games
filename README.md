# Best Selling Steam Games
SQL Intermediate 'Practice Loop' mini-project
<br>

### 🧼 Data Cleaning & Manipulation
- I split data into three CSV files based on where the field info came from - game_faqs, steam_main, steam_db. 
- I changed the format of the 'release_date' in Excel - to remove a comma in each row.
- I created a new table with SQL - to separate the multiple genre entries in each row of the 'user_defined_tags' field - named 'game_genres':
- I deleted 10 genre lines from game_genres. 
<br>

## Joins & Aggregates

### JOIN practice

I searched for the 10 game records with missing genre fields, to practice LEFT and RIGHT JOINs. 

```sql 

SELECT m.game_name, 
	g.genre
FROM steam_main AS m
LEFT JOIN game_genres AS g
	ON m.game_name = g.game_name
WHERE g.genre IS NULL; 

```

```sql 

SELECT m.game_name, 
	g.genre
FROM game_genres AS g
RIGHT JOIN steam_main AS m
	ON m.game_name = g.game_name
WHERE g.genre IS NULL; 

```

### Write a query using at least 2 JOINs. 

I searched records with all their game genres present and then filtered for difficulty over 3. 

```sql

SELECT m.game_name, 
	g.genre,
	f.difficulty
FROM steam_main AS m
LEFT JOIN game_genres AS g
	ON m.game_name = g.game_name
INNER JOIN game_faqs AS f
	ON m.game_name = f.game_name
WHERE g.genre IS NOT NULL 
	AND m.game_name IN (
		SELECT f.game_name
		FROM game_faqs AS f
		WHERE f.difficulty > 3
	)
ORDER BY f.difficulty DESC;

```

### Create a summary table using GROUP BY and COUNT/SUM/AVG.

Which developers have produced the most best-selling Steam games? 

```sql
SELECT developer,
	COUNT(developer) AS number_of_games
FROM steam_main
GROUP BY developer
ORDER BY number_of_games DESC
LIMIT 5;
```

<p align="left">
  <img src="images/top-developers.png" alt="Top Developers" width="500">
</p>

### Include a HAVING clause to filter based on aggregate.

Which genres have over 1 million downloads? 

```sql
SELECT g.genre,
	SUM(d.estimated_downloads) AS total_downloads
FROM game_genres AS g
INNER JOIN steam_db AS d
	ON g.game_name = d.game_name
GROUP BY g.genre
HAVING SUM(d.estimated_downloads) > 1000000
ORDER BY total_downloads DESC; 
```
<br>

## CASE Statements

### Use CASE in a SELECT to create a new category (e.g., “high-rated”, “low-rated”).

```sql
SELECT game_name,
	reviews_like_rate,
	CASE 
		WHEN reviews_like_rate > 49 THEN 'high-rated'
		ELSE 'low-rated'
		END AS rating_category
FROM steam_main
ORDER BY reviews_like_rate DESC;
```

### Use CASE in an ORDER BY to custom sort your results.

```sql
SELECT 
	game_name,
  	CASE 
  		WHEN supported_languages ILIKE '%Japanese%' THEN 'Supports Japanese'
    		ELSE 'Does NOT support Japanese'
  		END AS language_support
FROM steam_main
GROUP BY game_name
ORDER BY CASE 
		WHEN supported_languages ILIKE '%Japanese%' THEN 0
		ELSE 1
		END,
	game_name;
```
