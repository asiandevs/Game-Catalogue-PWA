##  Part 4 – Database Schema (`schema.sql`)

*From the “Full-Stack Annotated Study Guide: Game Catalogue PWA (SQLite + Node.js + HTML/CSS/JS)”*

---

### 🎯 Goal

This SQL script defines the **structure** of your SQLite database — the *blueprint* for how data is stored, related, and retrieved.

💡 **Analogy:**
Think of the database schema like a **blueprint for a library** —
each `CREATE TABLE` builds a new bookshelf, and each `FOREIGN KEY` defines how shelves relate.

**Annotation:** 
The games table uses INTEGER PRIMARY KEY AUTOINCREMENT for unique IDs.
title is NOT NULL to ensure every game has a name. Other fields are optional to
accommodate incomplete data. The INSERT statement populates sample data for testing.

---

###  Complete Annotated SQL Schema

```sql
-- ======================================================
--  schema.sql – Database design for Game Catalogue PWA
-- ======================================================

-- ----------------------------
-- 1️  Drop old tables if they exist (for clean rebuilds)
-- ----------------------------
DROP TABLE IF EXISTS games;
DROP TABLE IF EXISTS genres;
DROP TABLE IF EXISTS platforms;

--  Note:
-- This ensures you can re-run schema.sql multiple times without duplicate errors.

-- ----------------------------
-- 2️  Create Genres Table
-- ----------------------------
CREATE TABLE genres (
    id INTEGER PRIMARY KEY AUTOINCREMENT,  -- unique ID for each genre
    name TEXT NOT NULL UNIQUE               -- genre name (must be unique)
);

--  Example Data:
-- (1, 'Action'), (2, 'Adventure'), (3, 'RPG'), (4, 'Puzzle')

-- ----------------------------
-- 3️  Create Platforms Table
-- ----------------------------
CREATE TABLE platforms (
    id INTEGER PRIMARY KEY AUTOINCREMENT,  -- unique ID
    name TEXT NOT NULL UNIQUE              -- e.g., 'PC', 'PlayStation', 'Xbox', 'Switch'
);

-- ----------------------------
-- 4️  Create Games Table
-- ----------------------------
CREATE TABLE games (
    id INTEGER PRIMARY KEY AUTOINCREMENT,  -- unique ID for each game
    title TEXT NOT NULL,                   -- game title
    release_year INTEGER,                  -- release year (e.g., 2020)
    genre_id INTEGER,                      -- link to genres table
    platform_id INTEGER,                   -- link to platforms table
    developer TEXT,                        -- studio/developer name
    rating REAL,                           -- decimal rating (e.g., 8.5)
    FOREIGN KEY (genre_id) REFERENCES genres(id),      -- relationship to genres
    FOREIGN KEY (platform_id) REFERENCES platforms(id) -- relationship to platforms
);

--  Note:
-- FOREIGN KEY creates a link between tables.
-- Example: “The Witcher 3” (games) belongs to genre_id=3 (“RPG” in genres table).

-- ----------------------------
-- 5️  Insert Sample Data
-- ----------------------------

--  Genres
INSERT INTO genres (name) VALUES
('Action'),
('Adventure'),
('RPG'),
('Puzzle'),
('Sports');

--  Tip:
-- Use plural table names for consistency. Each row = one record in that category.

--  Platforms
INSERT INTO platforms (name) VALUES
('PC'),
('PlayStation'),
('Xbox'),
('Nintendo Switch');

--  Games
INSERT INTO games (title, genre, platform, release_year, developer) VALUES
    ('The Legend of Zelda', 'Action-Adventure', 'Nintendo Switch', 2017, 'Nintendo'),
    ('The Witcher 3', 'RPG', 'PC', 2015, 'CD Projekt Red'),
    ('Among Us', 'Party', 'Mobile', 2018, 'InnerSloth');

--  Pro Tip:
-- You can add more sample data easily with the same syntax.
```

---

### 🧩  Key Concepts Explained

| Concept              | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| **Table**            | A structured collection of related data (like a spreadsheet) |
| **Primary Key (PK)** | Unique ID for each record (auto-incremented number)          |
| **Foreign Key (FK)** | Links a record to another table’s primary key                |
| **NOT NULL**         | Field must contain a value (no blanks)                       |
| **UNIQUE**           | No two records can have the same value in that column        |
| **AUTOINCREMENT**    | Automatically generates the next available ID                |

💡 **Tip:**
SQLite allows you to explore the schema interactively:

```sql
.schema games       -- shows structure of the games table
```

---

###  Example Query Output

After running this schema, if you query:

```sql
SELECT title, release_year, name AS genre
FROM games
JOIN genres ON games.genre_id = genres.id;
```

You’ll get something like:

| title                    | release_year | genre  |
| ------------------------ | ------------ | ------ |
| The Witcher 3: Wild Hunt | 2015         | RPG    |
| God of War               | 2018         | Action |
| Halo Infinite            | 2021         | Action |

---

### 🧪 How to Run schema.sql

Inside your project directory:

```bash
cd database
sqlite3 games.db < schema.sql
```

✅ This command:

* Opens (or creates) `games.db`
* Runs every SQL statement in `schema.sql`
* Populates the database with tables and sample data

To verify:

```bash
sqlite3 games.db
.tables              # lists all tables
SELECT * FROM games; # view inserted records
```

---

### ✅ Outcome

After executing this script, you now have:

* 3 tables (`games`, `genres`, `platforms`)
* Proper relationships via foreign keys
* Example records ready for backend queries

