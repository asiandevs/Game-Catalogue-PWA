# 🎮 Game Catalogue PWA – Full-Stack Annotated Study Guide

*A complete beginner-friendly walkthrough of a Progressive Web App built with Node.js, SQLite, HTML, CSS, and JavaScript.*

---

## 📘 Overview

This repository provides a **step-by-step educational project** to help newcomers learn **full-stack web development** using real-world tools and best practices.

You’ll learn how to:
✅ Automate setup using Bash scripts
✅ Build a backend API using Node.js and Express
✅ Design and populate an SQLite database
✅ Create a responsive frontend with HTML, CSS, and JS
✅ Enable offline capabilities with a Progressive Web App (PWA)

---

## 🧭 Project Structure

```
game-catalogue-pwa/
│
├── css/                # Styling (layout, colors, responsiveness)
├── js/                 # Frontend logic and API integration
├── database/           # SQLite database and SQL scripts
├── documentation/      # Annotated learning guide parts
├── server.js           # Express + SQLite backend
├── package.json        # Node.js dependencies and scripts
├── setup-project.sh    # Bash script to create project scaffold
├── manifest.json       # PWA configuration
├── service-worker.js   # Offline caching logic
├── index.html          # Home page
├── catalogue.html      # Game listing page
├── about.html          # About/project info
└── README.md           # (You are here!)
```

---

## 🧩 Learning Path

This project is divided into **8 detailed parts**, each designed to build your knowledge gradually.
All files are located under `/docs/` or can be read directly on GitHub.

| Part                                                                             | Topic                                  | Description                                                   |
| -------------------------------------------------------------------------------- | -------------------------------------- | ------------------------------------------------------------- |
| [**Part 1 – Environment Setup & Overview**](part1_environment_setup.md)                 | Tool installation and folder structure | Learn to install Node.js, SQLite, VS Code, and Git            |
| [**Part 2 – Bash Project Setup Script**](part2_bash_setup.md)               | Automating setup                       | Understand how the script scaffolds the project automatically |
| [**Part 3 – Backend Code (`server.js`)**](part3_backend_code.md)                 | Node.js + Express + SQLite integration | Learn how to serve APIs and connect to the database           |
| [**Part 4 – Database Schema (`schema.sql`)**](part4_database_schema.md)     | Database design                        | Learn how to structure data and relationships in SQL          |
| [**Part 5 – Common Queries (`queries.sql`)**](part5_common_queries.md)             | Data operations                        | Retrieve, filter, and update data with SQL                    |
| [**Part 6 – SQLite Operations & Verification**](part6_sqlite_operations.md) | Testing and debugging                  | Learn to open, inspect, and verify your database              |
| [**Part 7 – Frontend (HTML, CSS, JS Overview)**](part7_frontend_overview.md)         | User interface                         | Build responsive and dynamic UI that fetches live data        |
| [**Part 8 – How It All Works Together**](part8_integration.md)              | End-to-end integration                 | Understand app architecture, PWA features, and deployment     |

---

## ⚙️ Quick Start

### 1️⃣ Clone the repository

```bash
git clone https://github.com/<your-username>/game-catalogue-pwa.git
cd game-catalogue-pwa
```

### 2️⃣ Run setup script

```bash
chmod +x setup-project.sh
./setup-project.sh
```

### 3️⃣ Install dependencies

```bash
npm install
```

### 4️⃣ Initialize the database

```bash
cd database
sqlite3 games.db < schema.sql
```

### 5️⃣ Run the backend

```bash
cd ..
node server.js
```

Backend runs at → [http://localhost:3000](http://localhost:3000)

---

## 💻 Live Preview (Frontend)

Use VS Code’s **Live Server** extension to open:

```
index.html
```

Your web app will connect to the local API and display all game data dynamically.

---

## 📱 Progressive Web App Features

✅ Works offline via Service Worker
✅ Installable on desktop/mobile
✅ Uses a lightweight SQLite database
✅ Fast and responsive UI built with pure JS

💡 **Try installing it:**

* In Chrome → Click the “Install App” icon in the address bar.
* Your Game Catalogue will appear like a native app.

---

## 🧠 Skills You’ll Practice

| Category          | Skills                                               |
| ----------------- | ---------------------------------------------------- |
| **Frontend**      | HTML5, CSS3 Grid, JavaScript (ES6), DOM manipulation |
| **Backend**       | Node.js, Express.js, REST APIs                       |
| **Database**      | SQLite, SQL queries, schema design                   |
| **DevOps Basics** | Bash scripting, environment setup, Git               |
| **PWA Concepts**  | Service workers, caching, manifest.json              |

---

## 🧩 Suggested Extensions

For the best experience, install these in VS Code:

* 🧱 **Live Server** – Preview HTML instantly
* 🧩 **SQLite Viewer** – Browse database visually
* ⚙️ **Prettier** – Auto-format your code
* 🔍 **ESLint** – Check for JS syntax issues

---

## 🏁 Conclusion

By completing all 8 parts, you’ll have built a **fully functional Progressive Web App** that demonstrates:

* Real-world full-stack architecture
* Clean separation of concerns
* Hands-on coding with modern web technologies

You can now proudly use this repository as:

* A **portfolio project**
* A **teaching aid**
* Or a **starter template** for future apps

---

**Next Step:**
👉 Explore `/docs/Part1_Setup.md` to begin your learning journey.

---
