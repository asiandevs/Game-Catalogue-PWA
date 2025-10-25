## 🔄 Part 8 – How It All Works Together

*From the “Full-Stack Annotated Study Guide: Game Catalogue PWA (SQLite + Node.js + HTML/CSS/JS)”*

---

### 🎯 Goal

Understand the **complete flow** of how the Game Catalogue PWA operates — from user interaction to database query — and how to deploy it as a lightweight, installable web app.

💡 **Analogy:**
Think of your system as a **restaurant workflow**:

* The **frontend** is the waiter (takes orders from users)
* The **backend** is the chef (processes and prepares data)
* The **database** is the pantry (stores all ingredients)

---

## 🧠 1. The Full Architecture

Here’s the logical overview of the entire system:

```
+------------------------+
|      Frontend UI       |
|  HTML + CSS + JS (PWA) |
|------------------------|
|  - Displays games list |
|  - Handles navigation  |
|  - Registers service   |
|    worker for offline  |
+-----------|------------+
            |
            v
+------------------------+
|       Backend API      |
|   Node.js + Express.js  |
|------------------------|
|  - Listens on port 3000 |
|  - Serves HTML & JS     |
|  - Handles /api routes  |
|  - Queries SQLite DB    |
+-----------|------------+
            |
            v
+------------------------+
|      SQLite Database   |
|    games.db + schema   |
|------------------------|
|  - Stores games info    |
|  - Tables: games,       |
|    genres, platforms    |
|  - Returns query data   |
+------------------------+
```

💡 **Key Point:**
All three components live locally — no internet or external server is required, making it ideal for classroom projects or demos.

---

## ⚙️ 2. Request Flow (Step-by-Step)

| Step | Action                                 | Example                                       |
| ---- | -------------------------------------- | --------------------------------------------- |
| 1️⃣  | User opens `catalogue.html` in browser | Browser loads frontend UI                     |
| 2️⃣  | `ui.js` calls `fetchGames()`           | JavaScript requests `/api/games`              |
| 3️⃣  | Express handles route `/api/games`     | Runs `db.all('SELECT * FROM games')`          |
| 4️⃣  | SQLite returns result rows             | JSON array sent back to browser               |
| 5️⃣  | `ui.js` receives data                  | Builds HTML cards dynamically                 |
| 6️⃣  | User views games on screen             | Data displayed beautifully in the grid layout |

💡 **Tip:**
This architecture is called a **three-tier application** — Presentation (UI), Logic (API), and Data (DB).

---

## 🚀 3. Progressive Web App (PWA) Features

PWAs behave like **installable native apps** using just web technologies.
Your app already has the core PWA files:

| File                | Purpose                                          |
| ------------------- | ------------------------------------------------ |
| `manifest.json`     | Defines app name, icons, theme color, start page |
| `service-worker.js` | Handles caching, offline mode, and updates       |

---

### 📱 Example: `manifest.json`

```json
{
  "name": "Game Catalogue PWA",
  "short_name": "GameCat",
  "start_url": "index.html",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#0d6efd",
  "icons": [
    {
      "src": "icons/icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "icons/icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

💡 **Note:**
Once this is registered in your HTML `<head>` and your service worker runs, browsers will allow users to **“Install App”** like a native application.

---

### ⚙️ Example: `service-worker.js`

```js
// =====================================================
//  service-worker.js – Offline caching for the PWA
// =====================================================

const CACHE_NAME = 'game-catalogue-v1';
const urlsToCache = [
  '/',
  '/index.html',
  '/catalogue.html',
  '/about.html',
  '/css/style.css',
  '/js/app.js',
  '/js/ui.js',
  '/js/database.js'
];

// Install event – cache core files
self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll(urlsToCache))
  );
  console.log(' Service Worker installed');
});

// Fetch event – serve from cache or fetch network
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request)
      .then(response => response || fetch(event.request))
  );
});
```

💡 **Tip:**
When offline, cached pages still load — this is what makes your PWA usable without internet access.

---

## 🧩 4. Local Deployment & Testing

### 🧪 Run the Backend

```bash
node server.js
```

✅ Server runs at → [http://localhost:3000](http://localhost:3000)

### 🌐 Test API Endpoint

Visit → [http://localhost:3000/api/games]
You should see JSON data output like:

```json
[
  { "title": "The Witcher 3", "rating": 9.8 },
  { "title": "God of War", "rating": 9.6 }
]
```

### 💻 Launch Frontend

Use VS Code’s **Live Server** extension:

* Right-click `index.html`
* Choose “Open with Live Server”

Your app should display the game list dynamically, pulling data from your local Express + SQLite backend.

---

## ☁️ 5. Optional Deployment Options

| Option                       | Description                            | Use Case                   |
| ---------------------------- | -------------------------------------- | -------------------------- |
| **Render.com / Railway.app** | Free Node.js hosting                   | Quick public demo          |
| **Vercel / Netlify**         | Frontend hosting only (static HTML/JS) | Split API + UI deployment  |
| **Heroku / Fly.io**          | Full-stack hosting (Express + DB)      | Small-scale public app     |
| **Local Server (Node)**      | Run locally for classroom use          | Fastest setup for students |

💡 **Note:**
If you deploy online, switch to **a cloud database** (like PostgreSQL) or use **SQLite file persistence** carefully (since some hosts reset files).

---

## 🧠 6. Best Practices Recap

| Category            | Best Practice                                      |
| ------------------- | -------------------------------------------------- |
| **Database**        | Normalize tables; use foreign keys properly        |
| **Backend**         | Use async/await and error handling                 |
| **Frontend**        | Separate logic (UI, API, Styles) cleanly           |
| **PWA**             | Cache assets selectively to avoid stale data       |
| **Version Control** | Commit small, frequent changes with clear messages |

💡 **Example Commit Message:**

```
feat: add API route for fetching games by platform
fix: corrected rating column type in schema.sql
```

---

## 🧩 7. What You’ve Built

✅ A **complete full-stack application** including:

* Automated setup via Bash script
* Express.js + SQLite backend
* Responsive HTML/CSS + JavaScript frontend
* Progressive Web App installability
* Clean modular structure for easy expansion

💡 **Next Steps:**

* Add search or filter functionality
* Implement user login with JWT or session cookies
* Deploy the app online (Render or Vercel + Railway combo)
* Add game images and more UI polish

---

## 🏁 Final Thoughts

Congratulations 🎉 — you’ve built a working **Progressive Web App** using modern web and backend technologies — all locally, with SQLite as your database.

This guide is now a **complete GitHub-ready educational project**, ideal for showcasing:

* Full-stack fundamentals
* Web + Database integration
* PWA best practices
* Code organization and documentation

---

✅ **End of Full-Stack Annotated Study Guide**

---
