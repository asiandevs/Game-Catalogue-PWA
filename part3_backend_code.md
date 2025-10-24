# Part 3: Backend Code (server.js)

This file is part of the Full-Stack Annotated Study Guide: Game Catalogue PWA repository. It covers the backend setup using Node.js and Express to serve API endpoints and static files. [Return to repository root](../).

## Express.js and SQLite Integration

Create `server.js` in the project root to handle API and static serving. Install dependencies:  
`npm init -y && npm install express sqlite3`.

```javascript
const express = require('express');
const sqlite3 = require('sqlite3').verbose();
const app = express();
const db = new sqlite3.Database('./database/games.db');

app.use(express.json());
app.use(express.static('.')); // Serve static files (HTML, CSS, JS)

app.get('/api/games', (req, res) => {
    db.all('SELECT games.*, genres.name AS genre, platforms.name AS platform FROM games JOIN genres ON games.genre_id = genres.genre_id JOIN platforms ON games.platform_id = platforms.platform_id', [], (err, rows) => {
        if (err) return res.status(500).json({ error: err.message });
        res.json(rows);
    });
});

app.listen(3000, () => console.log('Server running on port 3000'));
```

**Annotation:** Express is a minimal web framework for Node.js. sqlite3 module connects to the DB. This setup allows querying without CORS issues locally.

## Middleware and Static File Serving

- `app.use(express.json())`: Parses JSON requests
- `app.use(express.static('.'))`: Serves frontend files from root (e.g., access index.html at localhost:3000)

**Annotation:** Middleware processes requests. Static serving turns Node into a simple web server, ideal for development.

## API Route Explanation (/api/games)

- `GET /api/games`: Joins tables and returns all games as JSON with genre and platform names
- Error handling: Sends 500 on DB errors

**Annotation:** This endpoint enables frontend to fetch data. Expand with query params (e.g., `?genre=Action`) for filtering. Use async/await for cleaner code in production.
