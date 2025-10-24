# Part 6: SQLite Operations & Verification

This file is part of the Full-Stack Annotated Study Guide: Game Catalogue PWA repository. It explains how to interact with the SQLite database. [[Return to repository root](https://github.com/asiandevs/game-catalogue-pwa-guide/tree/main)].

## How to Create, Open, and Inspect Databases

1. **Navigate to database folder:**
   ```bash
   cd game-catalogue-pwa/database
   ```

2. **Create/Run Schema:**
   ```bash
   sqlite3 games.db < schema.sql
   ```

3. **Open SQLite Shell:**
   ```bash
   sqlite3 games.db
   ```

4. **Inspect Database:**
   ```sql
   .tables                    -- List tables
   .schema games              -- View table structure
   SELECT * FROM games;       -- View data
   SELECT * FROM genres;      -- View genres
   SELECT * FROM platforms;   -- View platforms
   ```

5. **Exit Shell:**
   ```sql
   .exit
   ```

**Annotation:** The SQLite shell is interactive for testing. File-based DB means no server process—easy for local development.

## Common Commands and Troubleshooting Tips

### Essential SQLite Commands:
```sql
.headers on                   -- Show column names
.mode column                  -- Formatted output
.mode csv                     -- CSV format for export
.output filename.csv          -- Redirect output to file
.help                         -- List all commands
PRAGMA foreign_keys = ON;     -- Enable foreign key constraints
```

### Troubleshooting:
- **"Table not found":** Re-run schema with `sqlite3 games.db < schema.sql`
- **Access denied:** Check file permissions in database folder
- **Foreign keys not working:** Ensure `PRAGMA foreign_keys = ON;` is set
- **Data not persisting:** Verify you're in the correct database file
- **Backup:** Always backup DB before destructive operations

**Annotation:** Use `PRAGMA foreign_keys = ON;` to enforce referential integrity. Check SQLite documentation for specific error codes. For production, consider adding transactions for data consistency.

- Enhanced the annotation with additional practical advice
- Made the content more actionable with clear command examples
- Maintained all original content while improving organization and completeness
