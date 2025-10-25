## 🧱 Part 7 – Frontend (HTML, CSS, JS Overview)

*From the “Full-Stack Annotated Study Guide: Game Catalogue PWA (SQLite + Node.js + HTML/CSS/JS)”*

---

### 🎯 Goal

Understand how your **frontend** (HTML, CSS, and JavaScript) connects to the backend and database.
This section explains each file’s role and shows **annotated examples** of structure, styling, and interactivity.

💡 **Analogy:**
If your backend is the *engine* of a car, then your frontend is the *dashboard and bodywork* — it’s what users touch, see, and drive.

---

### 🗂️ 1. File Overview

| File                  | Purpose                                        |
| --------------------- | ---------------------------------------------- |
| `index.html`          | Landing page (home)                            |
| `catalogue.html`      | Lists all games from database                  |
| `about.html`          | Static information page                        |
| `/css/style.css`      | Base styling, layout, typography               |
| `/css/responsive.css` | Mobile-friendly adjustments                    |
| `/js/app.js`          | Registers service worker & app logic           |
| `/js/database.js`     | Fetches data from backend (API calls)          |
| `/js/ui.js`           | Builds dynamic HTML components (tables, cards) |

---

## 🧩 2. HTML Structure

Below is a simplified, **annotated** `catalogue.html` file.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Game Catalogue</title>

  <!-- Link to external styles -->
  <link rel="stylesheet" href="css/style.css" />
  <link rel="stylesheet" href="css/responsive.css" />

  <!-- PWA manifest & icons -->
  <link rel="manifest" href="manifest.json" />
</head>
<body>

  <!-- Header -->
  <header>
    <h1> Game Catalogue</h1>
    <nav>
      <a href="index.html">Home</a>
      <a href="catalogue.html" class="active">Catalogue</a>
      <a href="about.html">About</a>
    </nav>
  </header>

  <!-- Main content area -->
  <main>
    <section id="game-list">
      <!-- JavaScript will populate games dynamically here -->
    </section>
  </main>

  <!-- Footer -->
  <footer>
    <p>&copy; 2025 Game Catalogue PWA</p>
  </footer>

  <!-- Load JavaScript at bottom for better performance -->
  <script src="js/database.js"></script>
  <script src="js/ui.js"></script>
  <script src="js/app.js"></script>
</body>
</html>
```

💡 **Notes:**

* `<main>` holds the dynamic content.
* `<header>` and `<footer>` stay consistent across pages.
* JS is loaded at the **bottom** to avoid blocking page rendering.

---

## 🎨 3. CSS Basics (`style.css`)

```css
/* =====================================================
    style.css – Base styling for Game Catalogue PWA
   ===================================================== */

body {
  font-family: Arial, sans-serif;
  background-color: #f8f9fa;  /* light gray background */
  color: #222;                /* dark text for contrast */
  margin: 0;
  padding: 0;
}

header {
  background: #0d6efd;       /* bootstrap-like blue */
  color: white;
  padding: 1rem;
  text-align: center;
}

nav a {
  color: white;
  text-decoration: none;
  margin: 0 1rem;
}

nav a.active {
  border-bottom: 2px solid white; /* show active page */
}

#game-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
  padding: 1rem;
}

.game-card {
  background: white;
  border-radius: 8px;
  padding: 1rem;
  box-shadow: 0 2px 6px rgba(0,0,0,0.1);
}

.game-card h2 {
  margin-top: 0;
  font-size: 1.2rem;
  color: #0d6efd;
}
```

💡 **Tips:**

* Use a **CSS grid** for responsive layouts.
* Keep color and spacing consistent across pages.
* The `.game-card` class is used to display each game fetched from the backend.

---

## 📱 4. Responsive Design (`responsive.css`)

```css
/* =====================================================
   📱 responsive.css – Mobile & tablet adjustments
   ===================================================== */

@media (max-width: 768px) {
  header {
    text-align: left;
    padding: 1rem;
  }

  nav a {
    display: block;
    margin: 0.5rem 0;
  }

  #game-list {
    grid-template-columns: 1fr;  /* single column on mobile */
  }
}
```

💡 **Note:**
Media queries adapt your layout for smaller screens — this is what makes your PWA mobile-friendly.

---

## ⚙️ 5. JavaScript Logic

### 🧩 `/js/database.js`

Handles data fetching from the backend API.

```js
// =====================================================
// ⚙️ database.js – Fetch data from Node.js + SQLite API
// =====================================================

const API_URL = '/api/games';

async function fetchGames() {
  try {
    const response = await fetch(API_URL);   // Fetch data from Express API
    const games = await response.json();     // Parse JSON response
    return games;
  } catch (error) {
    console.error(' Error fetching games:', error);
    return [];
  }
}
```

💡 **Tip:**
Always wrap `fetch` in `try/catch` to handle network errors gracefully.

---

### 🧱 `/js/ui.js`

Builds HTML cards dynamically using fetched data.

```js
// =====================================================
//  ui.js – Dynamically build the game list UI
// =====================================================

async function displayGames() {
  const container = document.getElementById('game-list');
  const games = await fetchGames();

  if (games.length === 0) {
    container.innerHTML = '<p>No games found.</p>';
    return;
  }

  // Create cards for each game
  container.innerHTML = games.map(game => `
    <div class="game-card">
      <h2>${game.title}</h2>
      <p><strong>Developer:</strong> ${game.developer}</p>
      <p><strong>Platform:</strong> ${game.platform_id}</p>
      <p><strong>Year:</strong> ${game.release_year}</p>
      <p><strong>Rating:</strong>  ${game.rating}</p>
    </div>
  `).join('');
}

// Initialize UI after page load
document.addEventListener('DOMContentLoaded', displayGames);
```

💡 **Note:**
The `map()` function iterates over all games and converts them into HTML cards — a key modern JavaScript pattern.

---

### 🚀 `/js/app.js`

Registers your PWA’s service worker.

```js
// =====================================================
// 🚀 app.js – Service Worker registration
// =====================================================

if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/service-worker.js')
      .then(reg => console.log(' Service Worker registered:', reg.scope))
      .catch(err => console.log(' Service Worker failed:', err));
  });
}
```

💡 **Tip:**
Service workers enable **offline functionality** and **asset caching**, turning your app into a real PWA.

---

## 🧠 6. Frontend-Backend Flow Summary

1. `catalogue.html` loads → browser runs `ui.js`
2. `ui.js` calls `fetchGames()` from `database.js`
3. `database.js` requests `/api/games` from `server.js`
4. `server.js` queries `games.db` via SQLite
5. JSON results returned → `ui.js` creates cards in `<main>`

💡 **Analogy:**
It’s like ordering food:

* `ui.js` = customer placing the order
* `database.js` = waiter carrying the order
* `server.js` + SQLite = kitchen preparing and serving

---

## ✅ Outcome

You now have:

* A responsive HTML/CSS layout
* Dynamic JavaScript fetching live data
* A connected front-end and back-end  
