## 📘 Part 1: Environment Setup and Project Overview

*From the “Full-Stack Annotated Study Guide: Game Catalogue PWA (SQLite + Node.js + HTML/CSS/JS)”*

---

### 🧰 1. Overview

This project is a **Progressive Web App (PWA)** that catalogs video games.
It combines multiple technologies to teach students **full-stack web development**.

| Layer    | Technology            | Purpose                                 |
| -------- | --------------------- | --------------------------------------- |
| Frontend | HTML, CSS, JavaScript | Builds the user interface               |
| Backend  | Node.js + Express     | Handles API requests                    |
| Database | SQLite3               | Stores games, genres, and platforms     |
| Tooling  | Bash + VS Code + Git  | Automates setup and manages source code |

💡 **Analogy:**
Think of the app as a library system:

* **Frontend** = the library counter where users search for books (games).
* **Backend** = the librarian who fetches and manages data.
* **Database** = the shelves storing all books.

---

### 🧑‍💻 2. Installing Development Tools (macOS example)

#### 🔹 Step 1 – Install VS Code

Visit 👉 [https://code.visualstudio.com/](https://code.visualstudio.com/)
Download **Mac Universal** → unzip → move **Visual Studio Code.app** to `/Applications`.

💡 **Tip:**
VS Code is your “command center” — you’ll edit, run, and debug all code here.

---

#### 🔹 Step 2 – Install Node.js

Visit 👉 [https://nodejs.org/](https://nodejs.org/)
Download the **LTS (Long Term Support)** version and run the `.pkg` installer.

Verify installation:

```bash
node --version   # Should print something like v20.x.x
npm --version    # npm comes bundled with Node.js
```

💡 **Note:**
`node` runs JavaScript outside the browser.
`npm` (Node Package Manager) installs project dependencies (like Express or SQLite).

---

#### 🔹 Step 3 – Verify SQLite3

SQLite is pre-installed on macOS. Check version:

```bash
sqlite3 --version   # Outputs the SQLite version number
```

⚙️ **If missing:**
Install using Homebrew → `brew install sqlite3`

💡 **Tip:**
SQLite is a lightweight, file-based database — perfect for prototypes or local apps.
All data lives in one file (e.g., `games.db`).

---

#### 🔹 Step 4 – Install VS Code Extensions

Open VS Code → click **Extensions** icon or press `Cmd + Shift + X`.
Install the following:

| Extension                    | Purpose                               |
| ---------------------------- | ------------------------------------- |
| `SQLite` by alexcvzz         | Browse and query `.db` files visually |
| `Live Server` by Ritwick Dey | Preview HTML files instantly          |
| `ESLint` by Microsoft        | Linting and syntax checking for JS    |
| `Prettier – Code Formatter`  | Automatically format code             |

💡 **Best Practice:**
After installing, reload VS Code to activate them.

---

#### 🔹 Step 5 – Install Git

Git tracks your code changes — essential for version control and GitHub uploads.

```bash
git --version
# If missing:
# brew install git
```

Then configure your identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

💡 **Tip:**
You’ll later push this project to a GitHub repository for collaboration or submission.

---

### 🗂️ 3. Understanding Project Folder Structure

Once the setup script runs (next part), your folder tree will look like this:

```
game-catalogue-pwa/
│
├── css/                  # Stylesheets (look & feel)
│   ├── style.css
│   └── responsive.css
│
├── js/                   # Frontend JavaScript
│   ├── app.js
│   ├── database.js
│   └── ui.js
│
├── database/             # SQLite database and SQL files
│   ├── games.db
│   ├── schema.sql
│   └── queries.sql
│
├── icons/                # App icons for manifest
├── images/               # Game cover images
│
├── documentation/        # Assignment docs (diary, charts, etc.)
│
├── index.html            # Home page
├── catalogue.html        # Game list page
├── about.html            # About page
│
├── manifest.json         # PWA metadata
├── service-worker.js     # Offline caching logic
│
├── server.js             # Node.js backend
├── package.json          # Project dependencies
├── setup-project.sh      # Automation script
└── README.md             # Documentation (this guide)
```

💡 **Note:**
This structure keeps each layer separate — styling, logic, data, and documentation — which is a core best practice in software engineering.

---

### 🔗 4. Workflow Overview

1. **Run the Bash script** to create the folder skeleton.
2. **Install dependencies** (`npm install`) using `package.json`.
3. **Initialize SQLite database** by executing `schema.sql`.
4. **Start the backend server** (`node server.js`).
5. **Serve and test the app** with **Live Server** (frontend) or by hitting the API endpoint at `http://localhost:3000/api/games`.

💡 **Analogy:**
Imagine building a house:

* Bash script = lays the foundation (folders & files)
* SQLite schema = builds the rooms (tables & data)
* Node.js backend = installs the wiring (logic & data flow)
* HTML/CSS/JS = paints and furnishes the house (UI/UX)

---

### ✅ 5. Next Steps

In **Part 2**, you’ll learn how the Bash automation script works (`setup-project.sh`) —
how each command creates your project’s foundation automatically.

---
