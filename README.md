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

I searched for the 10 game records with missing genre fields. 

SAMPLE FORMAT:
```sql 

SELECT m.game_name, 
	g.genre
FROM steam_main AS m
LEFT JOIN game_genres AS g
	ON m.game_name = g.game_name
WHERE g.genre IS NULL; 

```

