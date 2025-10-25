# Part 4: Database Schema and Setup

This file is part of the **Full-Stack Annotated Study Guide: Game Catalogue PWA**  
repo. It defines the SQLite database schema for the game catalogue and explains its  
structure. See [README.md](../README.md) for the full guide.

## Database Schema

The SQLite database (`games.db`) stores game data in tables for `games`, `genres`,  
and `platforms`, with relationships via foreign keys.

*Annotation*: This schema includes three tables: `genres` for game genres,  
`platforms` for gaming platforms, and `games` linking to both via foreign keys.  
Dropping tables ensures clean rebuilds. Sample data populates the tables for testing.

```sql
-- ----------------------------
--   Drop old tables if they exist (for clean rebuilds)
-- ----------------------------
DROP TABLE IF EXISTS games;
DROP TABLE IF EXISTS genres;
DROP TABLE IF EXISTS platforms;

-- ----------------------------
--   Create Genres Table
-- ----------------------------
CREATE TABLE genres (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL UNIQUE
);

-- ----------------------------
--   Create Platforms Table
-- ----------------------------
CREATE TABLE platforms (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL UNIQUE
);

-- ----------------------------
--   Create Games Table
-- ----------------------------
CREATE TABLE games (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    release_year INTEGER,
    genre_id INTEGER,
    platform_id INTEGER,
    developer TEXT,
    rating REAL,
    FOREIGN KEY (genre_id) REFERENCES genres(id),
    FOREIGN KEY (platform_id) REFERENCES platforms(id)
);

-- ----------------------------
--   Insert Sample Data
-- ----------------------------

INSERT INTO genres (name) VALUES
    ('Action'),
    ('Adventure'),
    ('RPG'),
    ('Puzzle'),
    ('Sports');

INSERT INTO platforms (name) VALUES
    ('PC'),
    ('PlayStation'),
    ('Xbox'),
    ('Nintendo Switch');

INSERT INTO games (title, genre_id, platform_id, release_year, developer, rating) VALUES
    ('The Legend of Zelda', 2, 4, 2017, 'Nintendo', 9.5),
    ('The Witcher 3', 3, 1, 2015, 'CD Projekt Red', 9.3),
    ('Among Us', 4, NULL, 2018, 'InnerSloth', 8.0);
