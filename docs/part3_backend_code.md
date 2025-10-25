##  Part 3 – Backend Code (`server.js`)

*From the “Full-Stack Annotated Study Guide: Game Catalogue PWA (SQLite + Node.js + HTML/CSS/JS)”*

---

### 🎯 Goal

This file starts a small **Express web server** that:

1. Connects to a **SQLite database**
2. Exposes a REST API endpoint (`/api/games`)
3. Serves your PWA’s static files

---

### 💻 Full Code with Inline Comments

```js
// ======================================================
//   server.js – Backend logic for Game Catalogue PWA
// ======================================================

// ---------------- Required Modules ----------------
const express = require('express');          // lightweight web framework for Node
const sqlite3 = require('sqlite3').verbose(); // SQLite driver (verbose = extra debug info)
const path = require('path');                 // built-in module to handle file paths

// ---------------- App Initialization ----------------
const app = express();    // create an Express application
const PORT = 3000;        // server will listen on http://localhost:3000

// ---------------- Middleware ----------------
app.use(express.json());          // parses incoming JSON requests
app.use(express.static(__dirname)); // serves all files (html, css, js) in current dir

/*  Note:
   Middleware = “in-between” code that runs before routes.
   express.json() lets you send/receive JSON.
   express.static() turns the folder into a mini web server.
*/

// ---------------- Database Connection ----------------
const db = new sqlite3.Database('./database/games.db', (err) => {
  if (err) {
    console.error(' Error connecting to database:', err.message);
  } else {
    console.log(' Connected to SQLite database');
  }
});

/*  Tip:
   new sqlite3.Database(path, callback)
   - creates/opens the database file
   - if missing, SQLite creates it automatically
*/

// ---------------- Sample API Route ----------------
app.get('/api/games', (req, res) => {
  // run an SQL query and return results as JSON
  const sql = 'SELECT * FROM games';
  db.all(sql, [], (err, rows) => {
    if (err) {
      res.status(500).json({ error: err.message }); // 500 = server error
      return;
    }
    res.json(rows); // send array of games to browser
  });
});

/*  Note:
   db.all(sql, params, callback)
   - executes a SELECT query
   - returns all rows in an array (‘rows’)
   Perfect for read-only data fetches.
*/

// ---------------- Start Server ----------------
app.listen(PORT, () => {
  console.log(` Server running at http://localhost:${PORT}`);
});

/*  Analogy:
   Express = restaurant
   - app.get('/api/games') = waiter who takes orders
   - db.all() = chef who cooks data from the kitchen (database)
   - res.json() = plate served back to customer (browser)
*/
```

---

### 🧭 How to Run

```bash
npm install     # installs express and sqlite3 packages
node server.js  # starts server on port 3000
```

Then open → [http://localhost:3000/api/games](http://localhost:3000/api/games)
You should see JSON data (or an empty array until you build the database).

---

### 🧩 Key Concepts Recap

| Concept           | Description                                   |
| ----------------- | --------------------------------------------- |
| **Express App**   | Simplifies HTTP server creation               |
| **Middleware**    | Functions that process requests before routes |
| **Route Handler** | Defines what happens for a given URL          |
| **SQLite Driver** | Lets Node talk to a SQLite file               |
| **API Endpoint**  | URL returning JSON instead of HTML            |

💡 **Pro Tip:**
Add more routes like `/api/genres`, `/api/platforms`, or `/api/stats` by copying the same pattern.

---

### ✅ Outcome

You now have a live backend that:

* Serves web pages and static assets
* Connects to a SQLite database
* Returns game data via a REST API
