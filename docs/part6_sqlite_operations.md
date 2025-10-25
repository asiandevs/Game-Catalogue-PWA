##  Part 6 – SQLite Operations & Verification

*From the “Full-Stack Annotated Study Guide: Game Catalogue PWA (SQLite + Node.js + HTML/CSS/JS)”*

---

### 🎯 Goal

This section will teach you how to:

* Open your SQLite database manually
* Run and test SQL commands
* Inspect tables, data, and indexes
* Verify your schema and queries work correctly

💡 **Analogy:**
Think of the SQLite command-line as your **database control room** —
you can see all the tables, check their contents, and even repair issues if something breaks.

---

### 🧰 1. Opening the Database

Navigate to your database folder:

```bash
cd game-catalogue-pwa/database
```

Then open SQLite:

```bash
sqlite3 games.db
```

✅ You’ll see a prompt like this:

```
SQLite version 3.46.0 2025-10-25
Enter ".help" for usage hints.
sqlite>
```

💡 **Tip:**
At the `sqlite>` prompt, you can run SQL statements directly.
Commands starting with a `.` (dot) are **SQLite-specific commands**, not SQL.

---

### ⚙️ 2. Common SQLite Commands

```bash
.tables             # Lists all tables in the database
.schema games       # Shows SQL structure of the 'games' table
.headers on         # Display column names when showing results
.mode column        # Aligns columns neatly for readability
.exit               # Exits the SQLite CLI
```

💡 **Note:**
Always use `.headers on` and `.mode column` for clean output — it makes debugging easier.

---

### 🔍 3. Viewing Data

```sql
SELECT * FROM games;
```

✅ Example output:

```
id  title                        release_year  genre_id  platform_id  developer           rating
--  ----------------------------  ------------  --------  -----------  ------------------  -------
1   The Witcher 3: Wild Hunt      2015          3         1            CD Projekt Red      9.8
2   God of War                    2018          1         2            Santa Monica Studio 9.6
3   Halo Infinite                 2021          1         3            343 Industries      8.4
4   Animal Crossing: New Horizons 2020          4         4            Nintendo            9.0
5   FIFA 22                       2021          5         1            EA Sports           7.8
```

💡 **Tip:**
If the output looks messy, run these once:

```bash
.mode column
.headers on
```

---

### 🧩 4. Inspecting Table Relationships

To confirm that your **foreign keys** work properly:

```sql
PRAGMA foreign_key_list(games);
```

✅ This command shows which columns in `games` link to other tables:

| id | seq | table     | from        | to | on_update | on_delete | match |
| -- | --- | --------- | ----------- | -- | --------- | --------- | ----- |
| 0  | 0   | genres    | genre_id    | id | NO ACTION | NO ACTION | NONE  |
| 1  | 0   | platforms | platform_id | id | NO ACTION | NO ACTION | NONE  |

💡 **Pro Tip:**
If foreign keys aren’t being enforced, enable them manually:

```sql
PRAGMA foreign_keys = ON;
```

---

### 🧠 5. Validating Query Results

Let’s test one of your practical queries from `queries.sql`.

#### Example – Average Rating by Platform

```sql
SELECT p.name AS platform, ROUND(AVG(g.rating), 2) AS avg_rating
FROM games g
JOIN platforms p ON g.platform_id = p.id
GROUP BY p.name
ORDER BY avg_rating DESC;
```

✅ Expected output:

| platform        | avg_rating |
| --------------- | ---------- |
| PlayStation     | 9.6        |
| Nintendo Switch | 9.0        |
| PC              | 8.8        |
| Xbox            | 8.4        |

💡 **Tip:**
This query checks that your joins and numeric operations are working properly.

---

### 🧰 6. Importing & Exporting Data

#### Export to CSV

```bash
sqlite> .headers on
sqlite> .mode csv
sqlite> .output games_export.csv
sqlite> SELECT * FROM games;
sqlite> .output stdout
```

✅ You’ll now have `games_export.csv` in the same folder — openable in Excel or VS Code.

#### Import from CSV

```bash
sqlite> .mode csv
sqlite> .import games_export.csv games
```

⚙️ **Note:**
This replaces table content — always back up your database first.

---

### 🚧 7. Troubleshooting Common Errors

| Error Message                   | Meaning                                        | Fix                                                   |
| ------------------------------- | ---------------------------------------------- | ----------------------------------------------------- |
| `no such table: games`          | You haven’t run `schema.sql` yet               | Run `sqlite3 games.db < schema.sql`                   |
| `no such column`                | You misspelled a column name                   | Check `.schema table_name`                            |
| `database is locked`            | Another process (e.g. Node.js) is using it     | Close the app or wait, then retry                     |
| `FOREIGN KEY constraint failed` | You tried inserting invalid genre/platform IDs | Check your reference IDs with `SELECT * FROM genres;` |

💡 **Pro Tip:**
Always **backup** before modifying data — copy the `.db` file somewhere safe.

---

### 🧮 8. Useful Debug Queries

```sql
-- Count how many records per table
SELECT 'games' AS table_name, COUNT(*) FROM games
UNION ALL
SELECT 'genres', COUNT(*) FROM genres
UNION ALL
SELECT 'platforms', COUNT(*) FROM platforms;

-- Check distinct developers
SELECT DISTINCT developer FROM games;

-- See top 3 rated games
SELECT title, rating FROM games ORDER BY rating DESC LIMIT 3;
```

💡 These are excellent for sanity checks and debugging logic in your backend.

---

### ✅ Outcome

After completing this section, you can now:

* Open and explore your SQLite database
* Verify tables, columns, and foreign keys
* Test and validate your SQL queries
* Export or import data easily
