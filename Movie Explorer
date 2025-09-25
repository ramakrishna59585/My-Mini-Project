<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Movie Explorer</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #0d1117;
      color: #fff;
      margin: 0;
      padding: 0;
      text-align: center;
    }
    header {
      background: #161b22;
      padding: 20px;
    }
    h1 {
      margin: 0;
      color: #58a6ff;
    }
    #searchBox {
      margin: 20px;
      padding: 10px;
      width: 250px;
      border-radius: 5px;
      border: none;
    }
    #movieList, #favorites {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 15px;
      margin: 20px;
    }
    .movie-card {
      background: #21262d;
      border-radius: 10px;
      padding: 10px;
      width: 180px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.5);
      transition: transform 0.2s;
    }
    .movie-card:hover {
      transform: scale(1.05);
    }
    img {
      width: 100%;
      border-radius: 8px;
    }
    button {
      margin-top: 10px;
      padding: 6px 12px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      background: #238636;
      color: white;
    }
    button:hover {
      background: #2ea043;
    }
    h2 {
      margin-top: 30px;
      color: #f0f6fc;
    }
  </style>
</head>
<body>
  <header>
    <h1>🎬 Movie Explorer</h1>
    <input type="text" id="searchBox" placeholder="Search for movies...">
    <button onclick="searchMovies()">Search</button>
  </header>

  <h2>Search Results</h2>
  <div id="movieList"></div>

  <h2>⭐ Favorites</h2>
  <div id="favorites"></div>

  <script>
    const apiKey = "thewdb"; // Free demo key, replace with your OMDb key
    const movieList = document.getElementById("movieList");
    const favoritesDiv = document.getElementById("favorites");

    // Load favorites from localStorage
    let favorites = JSON.parse(localStorage.getItem("favorites")) || [];

    function searchMovies() {
      const query = document.getElementById("searchBox").value;
      if (!query) return alert("Enter a movie name!");
      fetch(`https://www.omdbapi.com/?s=${query}&apikey=${apiKey}`)
        .then(res => res.json())
        .then(data => {
          movieList.innerHTML = "";
          if (data.Search) {
            data.Search.forEach(movie => {
              const card = document.createElement("div");
              card.className = "movie-card";
              card.innerHTML = `
                <img src="${movie.Poster !== "N/A" ? movie.Poster : "https://via.placeholder.com/150"}">
                <h3>${movie.Title}</h3>
                <p>${movie.Year}</p>
                <button onclick="addToFavorites('${movie.imdbID}')">Add to Favorites</button>
              `;
              movieList.appendChild(card);
            });
          } else {
            movieList.innerHTML = "<p>No movies found</p>";
          }
        });
    }

    function addToFavorites(id) {
      if (!favorites.includes(id)) {
        favorites.push(id);
        localStorage.setItem("favorites", JSON.stringify(favorites));
        loadFavorites();
      }
    }

    function removeFromFavorites(id) {
      favorites = favorites.filter(fav => fav !== id);
      localStorage.setItem("favorites", JSON.stringify(favorites));
      loadFavorites();
    }

    function loadFavorites() {
      favoritesDiv.innerHTML = "";
      favorites.forEach(id => {
        fetch(`https://www.omdbapi.com/?i=${id}&apikey=${apiKey}`)
          .then(res => res.json())
          .then(movie => {
            const card = document.createElement("div");
            card.className = "movie-card";
            card.innerHTML = `
              <img src="${movie.Poster !== "N/A" ? movie.Poster : "https://via.placeholder.com/150"}">
              <h3>${movie.Title}</h3>
              <p>${movie.Year}</p>
              <button onclick="removeFromFavorites('${movie.imdbID}')">Remove</button>
            `;
            favoritesDiv.appendChild(card);
          });
      });
    }

    loadFavorites();
  </script>
</body>
</html>
