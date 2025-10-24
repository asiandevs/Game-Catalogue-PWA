# Part 2: Bash Project Setup Script (setup-project.sh)

This file is part of the Full-Stack Annotated Study Guide: Game Catalogue PWA repository. It explains the Bash script to automate the project folder structure setup. [[Return to repository root](https://github.com/asiandevs/game-catalogue-pwa-guide/tree/main)](../).

## Line-by-Line Breakdown of the Automation Script

The script automates folder and file creation. Save as `setup-project.sh`:

```bash
#!/bin/bash

# Create root folder
mkdir -p game-catalogue-pwa
cd game-catalogue-pwa

# Create subfolders
mkdir css js images database docs

# Create HTML files
touch index.html catalogue.html about.html

# Create JS files
touch js/app.js service-worker.js

# Create PWA config
touch manifest.json

# Create CSS
touch css/style.css

# Create database files
touch database/schema.sql database/queries.sql database/games.db

# Add sample content to schema.sql (example schema)
cat << EOF > database/schema.sql
CREATE TABLE genres (
    genre_id INTEGER PRIMARY KEY,
    name TEXT NOT NULL
);

CREATE TABLE platforms (
    platform_id INTEGER PRIMARY KEY,
    name TEXT NOT NULL
);

CREATE TABLE games (
    game_id INTEGER PRIMARY KEY,
    title TEXT NOT NULL,
    genre_id INTEGER,
    platform_id INTEGER,
    publisher TEXT,
    release_year INTEGER,
    rating REAL,
    price REAL,
    description TEXT,
    image_url TEXT,
    FOREIGN KEY (genre_id) REFERENCES genres(genre_id),
    FOREIGN KEY (platform_id) REFERENCES platforms(platform_id)
);

-- Insert sample data
INSERT INTO genres (name) VALUES ('Action'), ('RPG'), ('Strategy'), ('Adventure'), ('Simulation'), ('Sports'), ('Puzzle'), ('Horror'), ('Fighting'), ('Racing');
INSERT INTO platforms (name) VALUES ('PC'), ('PlayStation'), ('Xbox'), ('Nintendo Switch'), ('Mobile'), ('VR'), ('Arcade'), ('Retro');
-- Insert 10 games (example)
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
EOF

# Make script executable (already done if running this)
chmod +x ../setup-project.sh

echo "Project structure created!"
```

## What Each Command Does

- `#!/bin/bash`: Shebang to run with Bash
- `mkdir -p game-catalogue-pwa`: Creates root folder (`-p` prevents errors if exists)
- `cd game-catalogue-pwa`: Navigates into it
- `mkdir css js ...`: Creates subfolders
- `touch file.html ...`: Creates empty files
- `cat << EOF > file.sql`: Heredoc to write multi-line content to a file
- `chmod +x`: Makes the script executable
- `echo`: Prints success message

## Notes & Best Practices for Bash Scripting

- Use `-p` with `mkdir` for idempotency
- Heredocs (`<< EOF`) are great for multi-line strings like SQL
- Always add error handling (e.g., `|| echo "Error"`)
- Version control: Commit this script to Git for reproducibility
- Best practice: Keep scripts modular; test in a temp dir first

**Annotation:** Bash automates repetitive setup, saving time. For cross-platform, consider tools like npm scripts.

- Standardized spacing and section organization
- Maintained all original content while improving readability
- Ensured code blocks are properly formatted with language specification
