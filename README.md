# Netflix clone with HTML,CSS, JS.
Netflix Clone, we all use Netflix in our day to day life for watching Movie. And if you are just starting with web development. This project can be a good practice project for you. This netflix clone is a dynamic site and has everything you need for fullstack development practice. It runs on a Node.js server. It uses TMDB API for all data.

# Features:

1) Looks similar to Netflix.

2) Dynamic site run on Node.js server.

3)All data is coming from TMDB API.

4) Dedicated Dynamic Movies Info page.

5) Has movie trailers, and recommendations.

6) Has smooth card slider effect.

# CODE
As this is a node.js web app. We need NPM and Node.js in order to start with, so make sure you have them installed in your system.

# Folder Structure.

![e238jwve7avebhtexudz](https://user-images.githubusercontent.com/93249038/211522279-05806383-caf7-4219-b670-87b5eb1f3932.png)

# NPM Init
Let's start with initializing NPM. So outside public folder, In your root directory, open Command Prompt or terminal. And execute. npm init

It will ask you for some details. You can press enter to have default project details. After executing npm init you should see a package.json file.

Great Now install Some libraries that we need in order to create a server.

#Installing Libraries

After creating package.json file. Run this command.

 $ npm i express.js nodemon

i - means install.

express.js - is a library we need to create server.

nodemon - is a library which allow you to run server seamlessly even after making changes to the server.

After installation complete, you should be able to see node_modules folder in your root directory.

Now open package.json file in your text editor. And edit it a little bit.

Change the value on "main" key to "server.js".
main

Delete "test" cmd from "scripts" object. And add new cmd called "start" and set it value to "nodemon server.js".
scripts

# Server.js

After editing package.json create JS file server.js in the root directory.

And write this in server.js.
const express = require('express');
const path = require('path');

let initial_path = path.join(__dirname, "public");

let app = express();
app.use(express.static(initial_path));

app.get('/', (req, res) => {
    res.sendFile(path.join(initial_path, "index.html"));
})

app.listen(3000, () => {
    console.log('listening on port 3000......');
})
Explanation
In the top, we are using require method to import library so that we can use it in this file. We are importing two libraries express and path.

path library is used to track paths.

After done importing libraries. We are setting a variable app equal to express(), which enable all the server related features to our app variable. And we also have initial_path which is holding our public folder path.

After that we have, app.use() which is used as a middle ware And inside this we have express.static() which allow us to set our static directory path. In this case we are setting our public folder as a static path, because our HTML files are inside that folder.

app.get('/') is a listener, And in this case it is listening for a GET request to our root / path. And whenever we get any GET request on /. We will serve them index.html file. That's what res.sendFile() do.

And the last block of our server.js is app.listen which is used to add a server's listening port. In this case, we set it to 3000. So our server will run on localhost:3000. Not any other port.

Now in your terminal or cmd prompt. Run npm start to start the server. And, open your browser to localhost:3000. You'll be able to see index.html file.

So up until now we have created our server and successfully serving our index.html file to / path.

So let's do some front end work here. Now

# Home page.
So for our Home page, we will use these files. index.html, style.css, home.js, api.js, scroll.js.

Let's start from index.html file. Start typing basic HTML structure. And after that link style.css file. And let's create navbar first.
<!-- navbar -->
<nav class="navbar">
    <img src="img/logo.png" class="logo" alt="">
    <div class="join-box">
        <p class="join-msg">unlimited tv shows & movies</p>
        <button class="btn join-btn">join now</button>
        <button class="btn">sign in</button>
    </div>
</nav>
Make sure your server is running, if it is not then run npm start in your terminal.

Output
navbar

All the CSS properties I'll use are easy to understand. So i'll only explain you JS only. But if you have doubt in any part. Even in CSS. Feel free to ask me in discussions.

Now style the navbar

Output
navbar 2
Now create movie section.
<!-- main section -->
<header class="main">
    <h1 class="heading">movies</h1>
    <p class="info">Movies move us like nothing else can, whether they're scary, funny, dramatic, romantic or anywhere in-between. So many titles, so much to experience.</p>
</header>
And style it
.main{
    position: relative;
    margin-top: 60px;
    width: 100%;
    padding: 40px 2.5vw;
    color: #fff;
}

.heading{
    text-transform: capitalize;
    font-weight: 900;
    font-size: 50px;
}

.info{
    width: 50%;
    font-size: 20px;
    margin-top: 10px;
}
main-2
And we have to create a movie list element inside .main element, this will hold our same genres movie.
<div class="movie-list">

    <button class="pre-btn"><img src="img/pre.png" alt=""></button>

    <h1 class="movie-category">Popular movie</h1>

    <div class="movie-container">
        <div class="movie">
            <img src="img/poster.jpg" alt="">
            <p class="movie-title">movie name</p>
        </div>
    </div>

    <button class="nxt-btn"><img src="img/nxt.png" alt=""></button>

</div>
You can see here, we have pre-btn and nxt-btn with them we also have a movie-card element. Well, we will create movie card and list element all with JS but for styling purpose we are creating one card here. Just for the sake of CSS.


.pre-btn,
.nxt-btn{
    position: absolute;
    height: 200px;
    top: 50%;
    transform: translateY(-50%);
    width: 2.5vw;
    background: #181818;
    border: none;
    outline: none;
    opacity: 0;
}

.pre-btn{
    left: -2.5vw;
}

.nxt-btn{
    right: -2.5vw;
}

.pre-btn img,
.nxt-btn img{
    width: 20px;
    height: 20px;
    object-fit: contain;
}

.nxt-btn:hover,
.pre-btn:hover{
    opacity: 1;
}
Output
Capture-3

Once we are done styling our cards. we can commit them.
<header class="main">
    <h1 class="heading">movies</h1>
    <p class="info">Movies move us like nothing else can, whether they're scary, funny, dramatic, romantic or anywhere in-between. So many titles, so much to experience.</p>
    <!-- movie list -->
    <!-- <div class="movie-list">

        <button class="pre-btn"><img src="img/pre.png" alt=""></button>

        <h1 class="movie-category">Popular movie</h1>

        <div class="movie-container">
            <div class="movie">
                <img src="img/poster.jpg" alt="">
                <p class="movie-title">movie name</p>
            </div>
        </div>

        <button class="nxt-btn"><img src="img/nxt.png" alt=""></button>

    </div> -->
</header>
Our main section should look like this. As we are done with homepage.

Now add all JS files in index.html file. As we need them now.
<script src="js/api.js"></script>
<script src="js/scroll.js"></script>
<script src="js/home.js"></script>
Make sure you add these files in exactly same order.

Now go to TMDB Official Site TO create an API key. If you don't know how to create it. Watch This.

After creating API key paste it into api.js file

api.js
let api_key = "your api key";
And after that go to TMDB Documentation. And find these three HTTP links.

api.js
let api_key = "your api key";

let img_url = "https://image.tmdb.org/t/p/w500";
let genres_list_http = "https://api.themoviedb.org/3/genre/movie/list?";
let movie_genres_http = "https://api.themoviedb.org/3/discover/movie?";
img_url - is to fetch image. Because we'll get movie image's path id. For example if we got image id as 123 then the image url will be https://image.tmdb.org/t/p/w500/123
genres_list_http - is to fetch movie genres list so we don't have to fetch different genres movie manually.
movie_genres_http - is to fetch the movie having same genres.
After done with these HTTPs. Open home.js file.

home.js
# Explanation
Here, we are using fetch method to genres_list_http that we have declared in api.js file. And using new URLSearchParams for adding api_key parameters to the link. And after getting res we are converting it to JSON be res.json() and after converting it to JSON we got the fetched data. Inside that. before understanding what we are doing. First see our fetched data structure.

Capture-2

So as to understood the data structure. Now understand what we are doing after getting JSON data.
data.genres.forEach(item => {
    fetchMoviesListByGenres(item.id, item.name);
})
As we have an array of genres, we are looping through each and every genres using forEach method. And inside that we are calling fetchMoviesListByGenres(id, genres) which we'll create next.

Now fetch movies with genres.
const fetchMoviesListByGenres = (id, genres) => {
    fetch(movie_genres_http + new URLSearchParams({
        api_key: api_key,
        with_genres: id,
        page: Math.floor(Math.random() * 3) + 1
    }))
    .then(res => res.json())
    .then(data => {
        makeCategoryElement(`${genres}_movies`, data.results);
    })
    .catch(err =>  console.log(err));
}
# Explanation
Here we are doing the same, we are fetching data but in this case we are making request to movie_genres_http and adding some more parameters.
with_genres param will give us movie with only that genres for instance if our genres id if for comedy movies, then we'll only get comedy movies.
page param will give use what of the result we want and in this case we are using Math.random() to fetch some random page of movie result.

After getting the data, we are performing the same res.json() to covert it into JSON. And calling makeCategoryElement(category, data) which will create our movie categories. Same if you want you can console log the data structure.

Now create movie categories. But before that select our main element from HTML.
const main = document.querySelector('.main');
const makeCategoryElement = (category, data) => {
    main.innerHTML += `
    <div class="movie-list">

        <button class="pre-btn"><img src="img/pre.png" alt=""></button>

        <h1 class="movie-category">${category.split("_").join(" ")}</h1>

        <div class="movie-container" id="${category}">

        </div>

        <button class="nxt-btn"><img src="img/nxt.png" alt=""></button>

    </div>
    `;
    makeCards(category, data);
}
  # Explanation
In this function, we have two arguments one is category and second is data. So the first thing our function is doing is adding a .movie-list element to our main element using innerHTML. If you remember this we created in our HTML file but at last commented copy that code and paste it here. Make sure you use += not = because we don't want to re-write its HTML.

<h1 class="movie-category">${category.split("_").join(" ")}</h1>
if you see this line. First of all we are using JS template string if you don;t use that you'll be not able to write like this. So here as we had an h1 element. we are setting it's text to our category that we got at the start of the function. But we also performing some methods here.Let's see them in detail.

for instance, assume category is equal to comedy.

<h1 class="movie-category">${category}</h1> Then output will be - comdey_movies. But we don't wont _ that why we split it.
<h1 class="movie-category">${category.split("_")}</h1> Then it will not work because now we have an array ["comedy", "movies"]. That's why use join method to join the array.
<h1 class="movie-category">${category.split("_").join(" ")}</h1> Then the output will be - Comedy Movies
I hope you understood this.

And then we are setting up a unique id to movie-container element so we can add card to it later. And at the very last, we are calling makeCards(category, data) to make cards inside that movie container element.

Now create a cards.
const makeCards = (id, data) => {
    const movieContainer = document.getElementById(id);
    data.forEach((item, i) => {

    })
}
# Explanation
Inside this function, we are selecting the movie container element on the start using that id we got from the above function. And after that we are looping through data using forEach method. Inside that We are checking some condition.
if(item.backdrop_path == null){
   item.backdrop_path = item.poster_path;
   if(item.backdrop_path == null){
      return;
  }
}
This condition is checking, if we don't have movie backdrop image path in our result set it to poster_path and we don't have that too. Don't make the card. Sometime TMDB movie's data do not have image path in it that's why we are checking for it.

After that we have
movieContainer.innerHTML += `
<div class="movie" onclick="location.href = '/${item.id}'">
    <img src="${img_url}${item.backdrop_path}" alt="">
    <p class="movie-title">${item.title}</p>
</div>
`;
Here, we are using the innerHTML method to append the card HTML structure that we already made at the start. And again here also we are using template strings. If you see we have onclick event to movie-card element which, in that event we are using location.href to redirect user to movie page that we'll create next.
if(i == data.length - 1){
    setTimeout(() => {
        setupScrolling();
    }, 100);
}
And this is checking for the last cast. when we are done creating card. we are running setupScrolling() function to setup slider effect. We also have to create this.

# site is Live Now :  https://csb-bewj5j.vercel.app/
