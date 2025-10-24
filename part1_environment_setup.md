# Part 1: Environment Setup and Project Overview

This file is part of the Full-Stack Annotated Study Guide: Game Catalogue PWA repository. It covers setting up your development environment and understanding the project structure for building a Progressive Web App (PWA) using SQLite, Node.js, and HTML/CSS/JS. [Return to repository root](../).

## Installing VS Code, Node.js, SQLite

To build the Game Catalogue PWA, start by setting up your development tools on macOS. These form the foundation for coding, running servers, and managing the database.

### Install VS Code:

1. Visit [code.visualstudio.com](https://code.visualstudio.com/)
2. Download the "Mac Universal" version
3. Extract the .zip file and drag "Visual Studio Code" to your Applications folder
4. Launch VS Code from Applications

**Annotation:** VS Code is a lightweight, extensible code editor ideal for full-stack development. It supports extensions for syntax highlighting, debugging, and live previews, making it perfect for HTML/CSS/JS and Node.js workflows.

### Install Node.js:

1. Go to [nodejs.org](https://nodejs.org/)
2. Download the LTS (Long Term Support) version for stability
3. Open the .pkg file and follow the installer prompts, entering your admin password as needed
4. Verify installation in Terminal: `node --version` (expect something like v20.x.x) and `npm --version`

**Annotation:** Node.js enables server-side JavaScript, crucial for the backend. NPM (Node Package Manager) handles dependencies like Express. LTS ensures compatibility and security updates.

### Install SQLite3:

- SQLite3 is pre-installed on macOS. Verify with `sqlite3 --version` in Terminal
- If missing (rare), install via Homebrew: `brew install sqlite`

**Annotation:** SQLite is a lightweight, file-based relational database. It's serverless, making it ideal for PWAs where data persistence is needed without a full DBMS like MySQL. Here, it's used for storing game data locally.

## Understanding Folder Structure and Workflow

The project uses a structured folder layout created via a Bash script (see Part 2). Key folders include:

- `css/` for stylesheets
- `js/` for JavaScript logic
- `images/` for assets
- `database/` for SQLite files (e.g., games.db, schema.sql, queries.sql)
- Root files: index.html (home), catalogue.html, about.html, manifest.json (PWA config), service-worker.js (offline support)
- `docs/` for documentation

### Workflow:

1. Setup environment and folders
2. Initialize database with schema and sample data
3. Build backend server to expose API endpoints
4. Develop frontend pages with HTML/CSS/JS, fetching data via API
5. Add PWA features for offline access
6. Test with Live Server or direct browser opening

**Annotation:** This structure separates concerns (MVC-like: Model=DB, View=HTML/CSS, Controller=JS/Node). Workflow emphasizes automation (scripting) and iteration (edit in VS Code, preview with Live Server).

## Overview of Project Goals (How Backend + Frontend + Database Fit Together)

The goal is a responsive PWA for browsing a game catalogue, with features like searching, filtering, and offline viewing.

- **Database (SQLite):** Stores game data (titles, genres, platforms, etc.)
- **Backend (Node.js + Express):** Serves API endpoints to query the DB, handles static files (HTML/CSS/JS)
- **Frontend (HTML/CSS/JS):** Renders pages, fetches data via fetch API, updates UI dynamically
- **Integration:** Frontend calls backend APIs (e.g., `/api/games`), which query SQLite and return JSON. PWA elements (manifest, service worker) enable installation and caching for offline use

**Annotation:** This full-stack approach teaches data flow in web apps. It's scalable—start local, deploy to hosting like Heroku.
