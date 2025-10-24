# Part 7: Frontend (HTML, CSS, JS Overview)

This file is part of the Full-Stack Annotated Study Guide: Game Catalogue PWA repository. It covers the frontend structure for the game catalogue PWA. [Return to repository root](../).

## Structure of the Main Pages (Home, Catalogue, About)

### index.html (Home):

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Catalogue</title>
    <link rel="stylesheet" href="css/style.css">
    <link rel="manifest" href="manifest.json">
</head>
<body>
    <nav>
        <a href="index.html">Home</a>
        <a href="catalogue.html">Catalogue</a>
        <a href="about.html">About</a>
    </nav>
    <header>
        <h1>Welcome to Game Catalogue</h1>
    </header>
    <section id="features">
        <!-- 4 feature cards, e.g., Search, Filter, Offline, Responsive -->
        <div class="feature-card">Search Games</div>
        <div class="feature-card">Filter by Genre</div>
        <div class="feature-card">Offline Access</div>
        <div class="feature-card">Responsive Design</div>
    </section>
    <section id="stats">
        <!-- Stats populated via JS -->
        <p>Games: <span id="game-count">0</span></p>
    </section>
    <footer>© 2025 Game Catalogue</footer>
    <script src="js/app.js"></script>
    <script>
        if ('serviceWorker' in navigator) {
            navigator.serviceWorker.register('/service-worker.js');
        }
    </script>
</body>
</html>
```

- **catalogue.html:** Similar structure, with a grid for games (populated via JS fetch)
- **about.html:** Static info page with project details

**Annotation:** HTML5 semantic tags (nav, header, section) improve accessibility. PWA registration in script tag. Viewport meta tag ensures proper mobile rendering.

## Responsive Design Explained with Annotated CSS Snippets

Create `css/style.css`:

```css
/* Base styles */
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    line-height: 1.6;
}

/* Navigation */
nav {
    background: #333;
    color: white;
    display: flex;
    justify-content: space-around;
    padding: 1em;
}

nav a {
    color: white;
    text-decoration: none;
    padding: 0.5em 1em;
}

/* Mobile navigation */
@media (max-width: 600px) {
    nav {
        flex-direction: column;
        text-align: center;
    }
    /* Stack nav on small screens */
}

/* Feature grid */
#features {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    padding: 1em;
}

.feature-card {
    background: #f4f4f4;
    padding: 1.5em;
    border-radius: 8px;
    text-align: center;
}

/* Responsive images */
img {
    max-width: 100%;
    height: auto;
}

/* Game grid for catalogue */
.games-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 1rem;
    padding: 1rem;
}

