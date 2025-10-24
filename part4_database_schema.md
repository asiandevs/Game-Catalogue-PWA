# Part 4: Database Schema (schema.sql)

This file is part of the Full-Stack Annotated Study Guide: Game Catalogue PWA repository. It defines the SQLite database schema for the game catalogue. [[Return to repository root](https://github.com/asiandevs/game-catalogue-pwa-guide/tree/main)].

## Understanding SQL Statements

The schema defines tables, keys, and sample data. Run with:  
`sqlite3 games.db < schema.sql`

```sql
CREATE TABLE genres (
    genre_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT UNIQUE NOT NULL
);

CREATE TABLE platforms (
    platform_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT UNIQUE NOT NULL
);

CREATE TABLE games (
    game_id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    genre_id INTEGER,
    platform_id INTEGER,
    publisher TEXT,
    release_year INTEGER CHECK (release_year > 1900),
    rating REAL CHECK (rating BETWEEN 0 AND 10),
    price REAL CHECK (price >= 0),
    description TEXT,
    image_url TEXT,
    FOREIGN KEY (genre_id) REFERENCES genres(genre_id) ON DELETE SET NULL,
    FOREIGN KEY (platform_id) REFERENCES platforms(platform_id) ON DELETE SET NULL
);

-- Indexes for performance
CREATE INDEX idx_games_title ON games(title);
CREATE INDEX idx_games_genre ON games(genre_id);

-- Sample data
INSERT INTO genres (name) VALUES ('Action'), ('RPG'), ('Strategy'), ('Adventure'), ('Simulation'), ('Sports'), ('Puzzle'), ('Horror'), ('Fighting'), ('Racing');
INSERT INTO platforms (name) VALUES ('PC'), ('PlayStation'), ('Xbox'), ('Nintendo Switch'), ('Mobile'), ('VR'), ('Arcade'), ('Retro');

-- Insert 10 games
INSERT INTO games (title, genre_id, platform_id, publisher, release_year, rating, price, description, image_url) VALUES 
('The Legend of Zelda', 2, 4, 'Nintendo', 2017, 9.5, 59.99, 'Epic adventure game.', 'zelda.jpg'),
('Cyberpunk 2077', 2, 1, 'CD Projekt', 2020, 7.8, 49.99, 'Open-world RPG.', 'cyberpunk.jpg'),
('FIFA 23', 6, 2, 'EA Sports', 2022, 8.0, 69.99, 'Soccer simulation.', 'fifa.jpg'),
('Tetris', 7, 5, 'Tetris Holding', 1984, 9.0, 4.99, 'Classic puzzle game.', 'tetris.jpg'),
('God of War', 1, 2, 'Sony', 2018, 9.4, 39.99, 'Action-adventure epic.', 'gow.jpg'),
('SimCity', 5, 1, 'Maxis', 2013, 7.5, 29.99, 'City-building simulation.', 'simcity.jpg'),
('Street Fighter V', 9, 2, 'Capcom', 2016, 8.2, 29.99, 'Competitive fighting.', 'sfv.jpg'),
('Hollow Knight', 4, 4, 'Team Cherry', 2017, 9.3, 14.99, 'Metroidvania adventure.', 'hollow.jpg'),
('Forza Horizon 5', 10, 3, 'Playground Games', 2021, 9.1, 59.99, 'Open-world racing.', 'forza.jpg'),
('Resident Evil 4', 8, 2, 'Capcom', 2023, 9.2, 59.99, 'Survival horror.', 're4.jpg');
```

**Annotation:** `CREATE TABLE` defines structure. `CHECK` constraints validate data. `AUTOINCREMENT` auto-generates IDs.

## Primary & Foreign Keys Explained

- **Primary Key** (e.g., `game_id`): Unique identifier, ensures no duplicates
- **Foreign Key** (e.g., `genre_id`): Links tables, enforces referential integrity

**Annotation:** Keys normalize data, reducing redundancy. `ON DELETE SET NULL` prevents orphan records.

## Inserting Data and Indexing for Performance

- `INSERT INTO` adds rows
- Indexes (`CREATE INDEX`) speed up queries on common fields like title

**Annotation:** Sample data (10 genres, 8 platforms, 10 games) jumpstarts testing. Indexes are crucial for large datasets.

