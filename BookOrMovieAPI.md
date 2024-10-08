---
title: Golang Book or Movie Review APIs
layout: post
author: Rachel Wang
---
### Book & Movie Review API 📚 📽️
---

### What is this? 🎉
- Using data from the [Open Movie Database](https://www.omdbapi.com/) and [Open Library](https://openlibrary.org/), these APIs allow you to gather data about any movie or book title in the database. 
- I have built 3 APIs, including one that will recommend whether or not a user should read the book first or watch the movie first based on the ratings available.

- Github Repo is here: <a href="https://github.com/rachelwritingcode/book-or-movie-api"><i class="fa-brands fa-github fa-2xl"></i></a>

```json
{
    "Recommendation": "Read the book first, then watch the movie.",
    "Title": "The Hobbit",
    "BookRating": "8.52",
    "MovieRating": "6.8",
    "MoviePlot": "A homebody hobbit in Middle Earth gets talked into joining a quest with a group of dwarves to recover their treasure from a dragon.",
    "BookPlot": "The Hobbit is a tale of high adventure, undertaken by a company of dwarves in search of dragon-guarded gold. A reluctant partner in this perilous quest is Bilbo Baggins, a comfort-loving unambitious hobbit, who surprises even himself by his resourcefulness and skill as a burglar.Encounters with trolls, goblins, dwarves, elves, and giant spiders, conversations with the dragon, Smaug, and a rather unwilling presence at the Battle of Five Armies are just some of the adventures that befall Bilbo.Bilbo Baggins has taken his place among the ranks of the immortals of children’s fiction. Written by Professor Tolkien for his children, The Hobbit met with instant critical acclaim when published.",
    "Author": "",
    "Director": "Jules Bass, Arthur Rankin Jr.",
    "Actors": "Orson Bean, Richard Boone, Hans Conried, John Huston",
    "BookPublished": "1937",
    "MovieReleased": "1977",
    "MovieAwards": "1 win  2 nominations."
}

```

---

#### Project Motivation 🤓
Learn more about the following:
- Creating APIs with the golang echo web framework `[DONE]`
- Webscraping with golang colly web scraping framework `[DONE]`
- Testing with golang testify `[HALF DONE]`
- Deploying with serverless computing, AWS Lambda `[TODO]`

---

#### How to use this API 
- Set up an API key with the [OMDB API](https://www.omdbapi.com/) (Open Movie Database API) 
- Create a local.env file with the OMDB_API and OMDB_KEY variables populated 
- API runs on server port 8080, you can change this if you would like by modifying the [server.go](server/server.go) file .


---

#### API Routes 


**URL**:  `GET /getbook:title`

Example Query

```
GET http://localhost:8080/getbook?title=the%20hobbit
```
- The `/getbook` endpoint will provide information about the queried book.

Success Response
```json
{
    "Title": "The Hobbit",
    "Author": "",
    "Rating": "8.52",
    "Plot": "The Hobbit is a tale of high adventure, undertaken by a company of dwarves in search of dragon-guarded gold. A reluctant partner in this perilous quest is Bilbo Baggins, a comfort-loving unambitious hobbit, who surprises even himself by his resourcefulness and skill as a burglar.Encounters with trolls, goblins, dwarves, elves, and giant spiders, conversations with the dragon, Smaug, and a rather unwilling presence at the Battle of Five Armies are just some of the adventures that befall Bilbo.Bilbo Baggins has taken his place among the ranks of the immortals of children’s fiction. Written by Professor Tolkien for his children, The Hobbit met with instant critical acclaim when published.",
    "Year": "1937"
}
```

Fail Response
```json
{
    "Status": "Error",
    "Code": "400",
    "Message": "Unable to find this title"
}
```

 ---

**URL**:  `GET /getmovie:title`

Example Query
```
GET http://localhost:8080/getmovie?title=iron%20man
```
- The `/getmovie` endpoint will provide information about the queried movie.

Success Response
```json
{
    "Title": "iron man",
    "Rating": "7.9",
    "Actors": "Robert Downey Jr., Gwyneth Paltrow, Terrence Howard",
    "Director": "Jon Favreau",
    "Plot": "After being held captive in an Afghan cave, billionaire engineer Tony Stark creates a unique weaponized suit of armor to fight evil.",
    "ReleaseYear": "2008",
    "Awards": "Nominated for 2 Oscars. 21 wins  73 nominations total"
}
````

Fail Response
```json
{
    "Status": "Error",
    "Code": "400",
    "Message": "Unable to find this title"
}
```

---

**URL**:  `GET /getreccomendation:title`

- The `/getreccommendation` endpoint will provide a suggestion based on the rating of the book and movie about which one to read or watch first.


Example Query
```
http://localhost:8080/getrecommendation?title=the%20hobbit
```

Success Response
```json
{
    "Recommendation": "Read the book first, then watch the movie.",
    "Title": "The Hobbit",
    "BookRating": "8.52",
    "MovieRating": "6.8",
    "MoviePlot": "A homebody hobbit in Middle Earth gets talked into joining a quest with a group of dwarves to recover their treasure from a dragon.",
    "BookPlot": "The Hobbit is a tale of high adventure, undertaken by a company of dwarves in search of dragon-guarded gold. A reluctant partner in this perilous quest is Bilbo Baggins, a comfort-loving unambitious hobbit, who surprises even himself by his resourcefulness and skill as a burglar.Encounters with trolls, goblins, dwarves, elves, and giant spiders, conversations with the dragon, Smaug, and a rather unwilling presence at the Battle of Five Armies are just some of the adventures that befall Bilbo.Bilbo Baggins has taken his place among the ranks of the immortals of children’s fiction. Written by Professor Tolkien for his children, The Hobbit met with instant critical acclaim when published.",
    "Author": "",
    "Director": "Jules Bass, Arthur Rankin Jr.",
    "Actors": "Orson Bean, Richard Boone, Hans Conried, John Huston",
    "BookPublished": "1937",
    "MovieReleased": "1977",
    "MovieAwards": "1 win  2 nominations."
}
```
Failed Response
```json
{
    "Status": "Error",
    "Code": "400",
    "Message": "Unable to find this title"
}
```

---
#### How to run the API locally?

In the root directory of the repo type the following:

`go run main.go`

---

#### How to run tests?
In the root directory of the repo type the following:

`go test`

---

#### How to run this in AWS lambda?

__Coming soon...__
