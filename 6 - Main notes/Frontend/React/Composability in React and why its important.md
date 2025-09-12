
2025-06-25 17:44

Status:

Tags: [React](3%20-%20Tags/React.md)

---
# Composability in React and why its important


Sure! Here's the **Markdown index (just the headings)** of the combined notes:

## 📘 Table of Contents

- [What is Composability in React?](#what-is-composability-in-react)
- [Why It’s Important](#why-its-important)
- [Netflix as a Real-World Example of React Composability](#netflix-as-a-real-world-example-of-react-composability)
  - [Component Hierarchy](#component-hierarchy)
- [Vanilla JS Equivalent (No Framework)](#vanilla-js-equivalent-no-framework)
  - [HTML](#html)
  - [JS](#js)
- [React vs Vanilla JS: Feature Comparison](#react-vs-vanilla-js-feature-comparison)
- [Key Takeaway](#key-takeaway)

### 🧩 **What is Composability in React?**

**Composability** means building complex UIs by **combining small, reusable components**—like LEGO blocks.

#### 🧠 Why It’s Important:

| Benefit               | What it Enables                                    |
| --------------------- | -------------------------------------------------- |
| Reusability           | Build once, use everywhere (e.g., `<MovieCard />`) |
| Maintainability       | Isolate bugs and logic in small components         |
| Scalability           | Add new features by composing new components       |
| Separation of concern | Each piece handles one task (UI, logic, etc.)      |
| Collaboration         | Teams can build different parts in parallel        |

---

### 🍿 **Netflix as a Real-World Example of React Composability**

Netflix UI can be broken down into **components**:

#### 🧱 Component Hierarchy

```text
App
├── Navbar
├── HeroBanner
├── Row (e.g., "Trending Now")
│   ├── MovieCard
│   │   ├── Thumbnail
│   │   ├── Title
│   │   └── PlayButton
└── Footer
```

Each `Row` is composed of `MovieCard`s.  
Each `MovieCard` is composed of smaller parts like image, title, and a button.

```jsx
function Row({ title, movies }) {
  return (
    <div className="row">
      <h2>{title}</h2>
      <div className="movie-list">
        {movies.map(movie => <MovieCard {...movie} />)}
      </div>
    </div>
  );
}
```

---

## ⚙️ Vanilla JS Equivalent (No Framework)

To mimic React-style composition in plain JavaScript:

### ✅ HTML

```html
<div id="app"></div>
```

### ✅ JS

```js
const movies = [
  { id: 1, title: "Stranger Things", thumbnail: "thumb1.jpg" },
  { id: 2, title: "Extraction 2", thumbnail: "thumb2.jpg" },
  { id: 3, title: "Beef", thumbnail: "thumb3.jpg" },
];

function createMovieCard(movie) {
  const card = document.createElement('div');
  card.className = 'movie-card';

  const img = document.createElement('img');
  img.src = movie.thumbnail;

  const title = document.createElement('p');
  title.textContent = movie.title;

  card.appendChild(img);
  card.appendChild(title);
  return card;
}

function createRow(titleText, movieList) {
  const row = document.createElement('div');
  row.className = 'row';

  const title = document.createElement('h2');
  title.textContent = titleText;

  const movieListContainer = document.createElement('div');
  movieListContainer.className = 'movie-list';

  movieList.forEach(movie => {
    movieListContainer.appendChild(createMovieCard(movie));
  });

  row.appendChild(title);
  row.appendChild(movieListContainer);
  return row;
}

// Mount the row
document.getElementById('app').appendChild(createRow("Trending Now", movies));
```

---

## 🆚 React vs Vanilla JS: Feature Comparison

| Feature                 | React                   | Vanilla JS                    |
| ----------------------- | ----------------------- | ----------------------------- |
| Component Reuse         | ✅ Easy                  | 🟡 Requires manual functions  |
| Readability             | ✅ JSX is clean          | ❌ Verbose DOM code            |
| Structure & Scalability | ✅ Strong                | ❌ Hard to manage as app grows |
| Data Binding            | ✅ Easy with props/state | ❌ Manual                      |
| Virtual DOM             | ✅ Optimized rendering   | ❌ Direct DOM (slower)         |

---

## 🧠 Key Takeaway

React’s composability lets you:

- Treat your UI like a **hierarchy of components**
    
- Reuse, manage, and scale your app more easily
    
- Avoid messy, repetitive DOM manipulation
    

Vanilla JS can mimic this structure, but **becomes hard to maintain** as complexity grows.

---
## References
[Exporting and Importing components in React - Composability](6%20-%20Main%20notes/Frontend/React/Exporting%20and%20Importing%20components%20in%20React%20-%20Composability.md)
[Why do we need to different files (index.jsx and app.jsx) in React projects](6%20-%20Main%20notes/Frontend/React/Why%20do%20we%20need%20to%20different%20files%20(index.jsx%20and%20app.jsx)%20in%20React%20projects.md) 