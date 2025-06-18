# Best Selling Steam Games
SQL Intermediate 'Practice Loop' mini-project


### 🧼 Data Cleaning
- I split data into three CSV files based on where the field info came from - game_faqs, steam_main, steam_db. 
- I changed the format of the 'release_date' in Excel - to remove a comma in each row.
- I created a new table with SQL - to separate the multiple genre entries in each row of the 'user_defined_tags' field - named 'game_genres':

sql

CREATE TABLE game_genres (
    game_name TEXT,
    genre TEXT
);

## Joins & Aggregates
