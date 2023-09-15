# Movie-Search-App-using-js
## Hosted Link :- https://rohitdhawale07.github.io/Movie-Search-App-using-js/movie.html
Creating a movie search app using HTML, CSS, and JavaScript is a great project to learn web development fundamentals. 
This app will allow users to search for movies by title and display information about the movies they search for. 
Below is a step-by-step guide to building this app with explanations:
We start by creating an HTML structure for our app. 
In the section, we include a reference to an external CSS file called "style.css" The

contains a title, an input field for searching, and a search button. 
The section is where we will display the search results. 
We include an external JavaScript file called "script.js" at the end of the body for handling functionality.

## HTML code
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Movie Search</title>
    <link rel="stylesheet" href="./style.css">
    <script defer src="./movie.js"></script>
</head>

<body>
    <div class="main">
        <div class="row" style="justify-content: center;">
            <input type="search" id="search" autofocus autocomplete="off" placeholder="Search here..." />
        </div>
        <div class="row" id="movie-box">

        </div>
    </div>
</body>

</html>
```
## CSS Code :-
```
@import url('https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,300;1,300&display=swap');
* {
    padding: 0;
    margin: 0;
    font-family: 'Lato', sans-serif;
    box-sizing: border-box;
}

.main {
    width: 100%;
    min-height: 100vh;
    background-color: black;
}

.row {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}

.box {
    padding: 10px;
    width: 25%;
    flex-basis: 25%;
    height: 400px;
    border-radius: 5px;
    overflow: hidden;
    border-radius: 5px;
    position: relative;
}

.box img {
    width: 100%;
    height: 100%;
    box-shadow: 0 4px 5px rgb(0 0 0 / 20%);
}

.box .overlay {
    width: 100%;
    max-height: 100%;
    min-height: auto;
    position: absolute;
    bottom: -100%;
    font-weight: bold;
    padding: 20px;
    border-radius: 10px 10px 0px 0px;
    left: 0;
    transition: 0.5s;
    background-color: white;
}

.box span {
    color: orange;
    display: inline-block;
    font-weight: bold;
    font-size: 25px;
}

.title {
    width: 100%;
    display: flex;
    justify-content: space-between;
}

.box:hover .overlay {
    bottom: 0%;
}

.overlay h2 {
    margin-bottom: 10px;
}

#search {
    width: 500px;
    padding: 5px 30px;
    background-color: rgba(52, 73, 94, 0.7);
    outline: none;
    border: none;
    box-shadow: 0px 0px 1px white;
    color: White;
    margin-top: 10px;
    font-size: 30px;
    border-radius: 25px;
    transition: 1s;
    margin-bottom: 15px;
}

#search:focus {
    background-color: white;
    color: black;
}
```

We start by selecting the HTML elements we need to work with using document.getElementById. 
We add an event listener to the search button to trigger the search when clicked. 
Inside the event listener, we fetch movie data from an API (you'll need to replace YOUR_API_KEY with a valid API key) based 
on the user's search term. 
The fetched data is processed in the displayMovies function, where we create and append movie cards to the movieList element. 
Important Note: In the JavaScript code, we've used the TMDB API for movie data. To use it, you'll need to sign up 
for an API key on the TMDB website and replace YOUR_API_KEY with your actual API key in the fetch URL.


This is a simple movie search app using HTML, CSS, and JavaScript. 
Users can enter a movie title, click the search button, and view movie results in a grid format. 
You can further enhance the app by adding features like pagination, more movie details, or even user accounts for saving favorite movies.



## JAVASCRIPT Code
```
const APIURL =
    "https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=04c35731a5ee918f014970082a0088b1&page=1";
const IMGPATH = "https://image.tmdb.org/t/p/w1280";
const SEARCHAPI =
    "https://api.themoviedb.org/3/search/movie?&api_key=04c35731a5ee918f014970082a0088b1&query=";


const moiveBox = document.querySelector("#movie-box")
const getMovies = async (url) => {
    const response = await fetch(url)
    const data = await response.json()
    showMovies(data)
}
getMovies(APIURL);


const showMovies = (data) => {
    moiveBox.innerHTML = "";
    data.results.forEach(
        (result) => {
            const imagePath = result.poster_path === null ? "img/image-missing.png" : IMGPATH + result.poster_path;
            // const box = `
            // <div class="box">
            //     <img src="${IMGPATH+result}" alt="" />
            //     <div class="overlay">
            //         <h2>Overview:</h2>
            //         Lorem ipsum, dolor sit amet consectetur adipisicing elit. Perspiciatis iste doloribus quam voluptatum, illum unde nostrum dignissimos, mollitia, sapiente porro natus neque cupiditate distinctio quod possimus aliquid reiciendis vel. Soluta?
            //     </div>
            // </div>
            // `
            const box = document.createElement("div")
            box.classList.add("box")
            box.innerHTML = `
                <img src="${imagePath}" alt="" />
                <div class="overlay">
                    <div class="title"> 
                        <h2> ${result.original_title}  </h2>
                        <span> ${result.vote_average} <span>
                    </div>
                    <h3>Overview:</h3>
                    <p> 
                        ${result.overview}
                    </p>
                 </div>
            `
            moiveBox.appendChild(box)
        }
    )
}

document.querySelector("#search").addEventListener(
    "keyup",
    function (event) {
        if (event.target.value != "") {
            getMovies(SEARCHAPI + event.target.value)
        } else {
            getMovies(APIURL);
        }
    }
)
```
