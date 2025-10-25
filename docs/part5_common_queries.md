## 🔍 Part 5 – Common Queries (`queries.sql`)

*From the “Full-Stack Annotated Study Guide: Game Catalogue PWA (SQLite + Node.js + HTML/CSS/JS)”*

---

### 🎯 Goal

This file contains **SQL commands** your backend can use to display, search, or modify data in the game catalogue.
Each query focuses on a common real-world operation — such as listing games, filtering by platform, or updating ratings.

💡 **Analogy:**
If your **database** is a library and **schema.sql** built the shelves,
then **queries.sql** is your librarian’s “playbook” — how they find, update, or report on books (games).

---

###  Complete Annotated SQL Queries

```sql
-- ======================================================
--  queries.sql – SQL queries for Game Catalogue PWA
-- ======================================================

-- ----------------------------
-- 1️ List all games
-- ----------------------------
SELECT * FROM games;

--  Note:
-- SELECT * means “get all columns” — useful for debugging but not ideal in production.
-- Prefer SELECT column1, column2, ... for efficiency.

-- ----------------------------
-- 2️ List all genres
-- ----------------------------
SELECT * FROM genres;

-- ----------------------------
-- 3️ List all platforms
-- ----------------------------
SELECT * FROM platforms;

-- ----------------------------
-- 4️ Show games with genre and platform names
-- ----------------------------
SELECT g.id, g.title, g.release_year,
       ge.name AS genre,
       p.name AS platform,
       g.developer, g.rating
FROM games g
JOIN genres ge ON g.genre_id = ge.id
JOIN platforms p ON g.platform_id = p.id
ORDER BY g.title;

--  Tip:
-- JOIN combines data across multiple tables.
-- “AS genre” renames the column for readability.
-- ORDER BY sorts alphabetically by title.

-- ----------------------------
-- 5️ Filter games by a specific genre (example: RPG)
-- ----------------------------
SELECT g.title, g.release_year, ge.name AS genre
FROM games g
JOIN genres ge ON g.genre_id = ge.id
WHERE ge.name = 'RPG';

--  Note:
-- WHERE filters records. 
-- This would list only games where genre = 'RPG'.

-- ----------------------------
-- 6️ Filter games released after a certain year
-- ----------------------------
SELECT title, release_year
FROM games
WHERE release_year >= 2020
ORDER BY release_year DESC;

--  Tip:
-- Use >=, <=, >, < for numeric comparisons.
-- DESC = descending order.

-- ----------------------------
-- 7️ Find all games for a particular platform (example: PlayStation)
-- ----------------------------
SELECT g.title, p.name AS platform
FROM games g
JOIN platforms p ON g.platform_id = p.id
WHERE p.name = 'PlayStation';

-- ----------------------------
-- 8️ Find games by a specific developer
-- ----------------------------
SELECT title, developer, rating
FROM games
WHERE developer = 'Nintendo';

-- ----------------------------
-- 9️ Show games with ratings above 9.0
-- ----------------------------
SELECT title, rating
FROM games
WHERE rating > 9.0
ORDER BY rating DESC;

--  Example Output:
-- | title                    | rating |
-- |---------------------------|--------|
-- | The Witcher 3: Wild Hunt  | 9.8    |
-- | God of War                | 9.6    |

-- ----------------------------
-- 10 Update a game’s rating
-- ----------------------------
UPDATE games
SET rating = 9.7
WHERE title = 'Halo Infinite';

--  Note:
-- UPDATE changes existing data.
-- Always use WHERE to limit which rows get updated!

-- ----------------------------
-- 11 Add a new game
-- ----------------------------
INSERT INTO games (title, release_year, genre_id, platform_id, developer, rating)
VALUES ('Elden Ring', 2022, 3, 1, 'FromSoftware', 9.5);

--  Tip:
-- INSERT adds new data. Column order must match VALUES order.

-- ----------------------------
-- 12️ Delete a game from the catalogue
-- ----------------------------
DELETE FROM games
WHERE title = 'FIFA 22';

--  Warning:
-- DELETE removes data permanently unless wrapped in a transaction.
-- Always double-check your WHERE clause.

-- ----------------------------
-- 13️ Count how many games per genre
-- ----------------------------
SELECT ge.name AS genre, COUNT(g.id) AS total_games
FROM games g
JOIN genres ge ON g.genre_id = ge.id
GROUP BY ge.name
ORDER BY total_games DESC;

--  Explanation:
-- GROUP BY groups rows by genre.
-- COUNT counts how many games fall in each genre.

-- ----------------------------
-- 14️ Get average rating by platform
-- ----------------------------
SELECT p.name AS platform, ROUND(AVG(g.rating), 2) AS avg_rating
FROM games g
JOIN platforms p ON g.platform_id = p.id
GROUP BY p.name
ORDER BY avg_rating DESC;

--  Tip:
-- AVG() = average, ROUND(value, 2) limits to 2 decimal places.

-- ----------------------------
-- 15️ Find the most recently released game
-- ----------------------------
SELECT title, release_year
FROM games
ORDER BY release_year DESC
LIMIT 1;

--  Note:
-- LIMIT restricts how many rows are returned.
-- Useful when you only need one result (like "latest game").
```

---

### 🧠 Concept Summary

| SQL Keyword                  | Meaning                                            |
| ---------------------------- | -------------------------------------------------- |
| **SELECT**                   | Reads data from a table                            |
| **FROM**                     | Specifies the table                                |
| **JOIN**                     | Combines data from multiple tables                 |
| **WHERE**                    | Filters results                                    |
| **ORDER BY**                 | Sorts results ascending (ASC) or descending (DESC) |
| **GROUP BY**                 | Groups similar records for aggregation             |
| **COUNT / AVG**              | Performs calculations across rows                  |
| **INSERT / UPDATE / DELETE** | Modifies database content                          |

💡 **Pro Tip:**
When experimenting, always start with `SELECT` before running `UPDATE` or `DELETE` — to confirm which rows you’ll affect.

---

### 🧪 How to Run These Queries

```bash
cd database
sqlite3 games.db
.read queries.sql   # execute all queries
```

To run one query manually:

```sql
SELECT * FROM games WHERE rating > 9.0;
```

---

### ✅ Outcome

After working through `queries.sql`, you can now:

* Retrieve, filter, and sort game data
* Insert and update records safely
* Combine data across multiple tables
* Generate statistics (counts, averages) 

Would you like me to continue with **Part 6 – SQLite Operations & Verification** in the same GitHub-ready annotated Markdown format next?
