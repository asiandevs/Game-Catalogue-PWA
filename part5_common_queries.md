# Part 5: Common Queries (queries.sql)

This file is part of the Full-Stack Annotated Study Guide: Game Catalogue PWA repository. It provides sample SQL queries for the game catalogue database. [[Return to repository root](https://github.com/asiandevs/game-catalogue-pwa-guide/tree/main)].

## Detailed Explanation of 15 Sample Queries

Create `database/queries.sql` with these for reference. They cover CRUD and advanced operations.

```sql
-- 1. All Games
SELECT * FROM games;

-- 2. Games by Genre
SELECT games.*, genres.name AS genre FROM games JOIN genres ON games.genre_id = genres.genre_id WHERE genres.name = 'Action';

-- 3. Games by Platform
SELECT games.*, platforms.name AS platform FROM games JOIN platforms ON games.platform_id = platforms.platform_id WHERE platforms.name = 'PC';

-- 4. Top Rated Games
SELECT * FROM games ORDER BY rating DESC LIMIT 5;

-- 5. Search by Title
SELECT * FROM games WHERE title LIKE '%Zelda%';

-- 6. Average Rating
SELECT AVG(rating) AS avg_rating FROM games;

-- 7. Count by Genre
SELECT genres.name, COUNT(*) AS game_count FROM games JOIN genres ON games.genre_id = genres.genre_id GROUP BY genres.name;

-- 8. Games Released After Year
SELECT * FROM games WHERE release_year > 2020;

-- 9. Update Rating
UPDATE games SET rating = 9.0 WHERE game_id = 1;

-- 10. Delete Game
DELETE FROM games WHERE game_id = 1;

-- 11. Insert New Game
INSERT INTO games (title, genre_id, platform_id, publisher, release_year, rating, price, description, image_url) 
VALUES ('New Game', 1, 1, 'Indie', 2025, 8.5, 19.99, 'New title.', 'newgame.jpg');

-- 12. Join All Tables
SELECT games.title, genres.name AS genre, platforms.name AS platform 
FROM games 
JOIN genres ON games.genre_id = genres.genre_id 
JOIN platforms ON games.platform_id = platforms.platform_id;

-- 13. Min/Max Price
SELECT MIN(price) AS min_price, MAX(price) AS max_price FROM games;

-- 14. Games with Images
SELECT * FROM games WHERE image_url IS NOT NULL;

-- 15. Complex Filter
SELECT * FROM games WHERE rating > 8 AND price < 50 ORDER BY release_year DESC;
```

## Filtering, Joining, Searching, and Updating Data

- **Filtering:** WHERE clause narrows results
- **Joining:** Combines related data across tables
- **Searching:** LIKE for pattern matching
- **Updating:** SET with WHERE modifies data

**Annotation:** Test queries in SQLite shell. Use prepared statements in code to prevent SQL injection.
- Maintained all original SQL content and structure
- Ensured annotations are properly formatted
- Made the query descriptions more scannable with clear categories
