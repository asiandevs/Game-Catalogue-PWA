## ⚙️ Part 2 – Bash Project Setup Script (`setup-project.sh`)

*From the “Full-Stack Annotated Study Guide: Game Catalogue PWA (SQLite + Node.js + HTML/CSS/JS)”*

---

### 🧩 1. Purpose of the Script

This Bash script automates the creation of every folder, file, and configuration needed for your **Progressive Web App**.
Instead of manually clicking “New Folder → New File,” the script does everything in seconds.

💡 **Analogy:**
Think of it as a *factory assembly line*—you press one button and your project skeleton is built.

---

### 🧰 2. Complete Script with Inline Comments

```bash
#!/bin/bash
# Tells the system this file should be executed using the Bash shell.

# ==============================
#  PWA Game Catalogue Setup
# ==============================

echo "Creating Game Catalogue PWA Project Structure..."
# echo prints messages to the terminal.

# ------------------------------
#  Create Main Project Folder
# ------------------------------

PROJECT_NAME="game-catalogue-pwa"   # Declare a variable for reuse
mkdir $PROJECT_NAME                 # mkdir = make directory
cd $PROJECT_NAME                    # cd = change into that directory

# Tip:
# Using variables lets you reuse names easily if you want to build
# a similar project later—just change PROJECT_NAME once.

# ------------------------------
# Create Folder Structure
# ------------------------------

echo "Creating folders..."

mkdir css js images icons database documentation
# Creates multiple folders in one line.

# ------------------------------
# Create HTML Files
# ------------------------------

echo "Creating HTML files..."

touch index.html catalogue.html about.html
# touch = create empty files if they don’t exist.

# ------------------------------
# Create CSS Files
# ------------------------------

echo "Creating CSS files..."

touch css/style.css css/responsive.css
# These will define your design and layout rules.

# ------------------------------
# Create JavaScript Files
# ------------------------------

echo "Creating JavaScript files..."

touch js/app.js js/database.js js/ui.js
# app.js  – main logic & service-worker registration
# database.js – handles DB API calls
# ui.js – updates the user interface dynamically

# ------------------------------
# Create Database Files
# ------------------------------

echo "Creating database file..."

touch database/games.db database/schema.sql database/queries.sql
# games.db – SQLite file (created automatically when used)
# schema.sql – table definitions
# queries.sql – reusable SQL statements

# ------------------------------
# Create PWA Config Files
# ------------------------------

echo "Creating PWA files..."

touch manifest.json service-worker.js
# manifest.json – metadata for installable app
# service-worker.js – enables offline caching

# ------------------------------
# Create Documentation Files
# ------------------------------

echo "Creating documentation files..."

touch documentation/process-diary.md \
      documentation/gantt-chart.md \
      documentation/storyboard.md

# These are often required for school/assessment deliverables.

# ------------------------------
# Create README.md
# ------------------------------

cat > README.md << 'EOF'
# Game Catalogue PWA
First part of read me

Created: $(date)
EOF
# cat > << 'EOF' ... EOF writes multiple lines to a file in one go.
# $(date) prints the current date/time.

# ------------------------------
# Create package.json for Node Dependencies
# ------------------------------

cat > package.json << 'EOF'
{
  "name": "game-catalogue-pwa",
  "version": "1.0.0",
  "description": "A PWA for cataloguing video games",
  "main": "index.js",
  "scripts": {
    "start": "node server.js"
  },
  "keywords": ["pwa", "games", "catalogue"],
  "author": "Monowar Mukul",
  "license": "MIT",
  "dependencies": {
    "express": "^4.18.2",
    "sqlite3": "^5.1.6"
  }
}
EOF
# package.json tells Node which packages to install and how to start the server.

# ------------------------------
# Create Simple Express Server
# ------------------------------

cat > server.js << 'EOF'
// Simple Express server for PWA
const express = require('express');          // Web framework
const sqlite3 = require('sqlite3').verbose(); // SQLite driver
const path = require('path');                 // Handles file paths

const app = express();                       // Initialize Express
const PORT = 3000;                           // Port number for server

// ---------------- Middleware ----------------
app.use(express.json());                     // Parse JSON bodies
app.use(express.static(__dirname));          // Serve static files

// ---------------- Database Connection ----------------
const db = new sqlite3.Database('./database/games.db', (err) => {
    if (err) {
        console.error('Error connecting to database:', err);
    } else {
        console.log('Connected to SQLite database');
    }
});

// ---------------- API Endpoint ----------------
// GET /api/games → return all games
app.get('/api/games', (req, res) => {
    db.all('SELECT * FROM games', [], (err, rows) => {
        if (err) {
            res.status(500).json({ error: err.message });
            return;
        }
        res.json(rows); // send data as JSON
    });
});

// ---------------- Start Server ----------------
app.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}`);
});
EOF

# ------------------------------
# Final Output
# ------------------------------

echo ""
echo "Project structure created successfully!"
echo "Project location: $(pwd)"
echo ""
echo "Next steps:"
echo "1. cd $PROJECT_NAME"
echo "2. npm install"
echo "3. Open the folder in VS Code: code ."
echo ""
```

---

### 3. How to Run the Script

```bash
chmod +x setup-project.sh   # Make script executable
./setup-project.sh          # Run it
```

When it finishes, your complete directory tree will appear automatically.

---

### ⚙️ 4. Behind the Scenes

| Concept           | Description                                         |
| ----------------- | --------------------------------------------------- |
| **Variables**     | Reusable placeholders (`$PROJECT_NAME`)             |
| **Commands**      | `mkdir`, `touch`, `cat`, `echo` control file system |
| **Heredoc (EOF)** | Writes multi-line text into files easily            |
| **Permissions**   | `chmod +x` lets others execute the script           |
| **Automation**    | Eliminates manual file creation and typos           |

💡 **Pro Tip:**
Scripts like this are common in DevOps—when you deploy or scaffold new environments.

---

### 5. What You Achieved

After running this script, you now have:

* ✅ Folder structure for code, data, and docs
* ✅ Starter HTML, CSS, JS, and database files
* ✅ Configured Node project (`package.json`)
* ✅ Working Express + SQLite server boilerplate

---

### 🔜 Next Part

Proceed to **Part 3 – Backend Code (`server.js`)**,
where we’ll dive deeper into how Node.js + Express + SQLite work together.

---
