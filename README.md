# Pulling data from a DB and create a web page using Jquery

## Aim of the exercice

Simulate fetching data about movies from a data base that will be displayed on a page using jquery fetch function et loops with a button to display and hide information.

###

## 1. Create a Data Base

To fetch something, first we must have data. For that we will create a json file that will act as our data base.

We will fill the json file with an id, the title of a movie, the genre, the year it came out, the movie poster and we will create an array that will contain some characters and the name of the actors who played them.

    {
        "id": 1,
        "titre": "Alien",
        "type": "science-fiction/horror",
        "sortie": "1979",
        "poster": "https://www.themoviedb.org/t/p/original/vfrQk5IPloGg1v9Rzbh2Eg3VGyM.jpg",
        "acteur": [
            {
                "character": "Ripley",
                "actor": "Sigourney Weaver"
            },
            {
                "character": "Dallas",
                "actor": "Tom Skerritt"
            },
            {
                "character": "Lambert",
                "actor": "Veronica Cartwright"
            }
        ]
    }


## 2. Preparing the html

### The head:

Before doing anything on the html itself we must first start by importing the **Jquery** library to the page.

In this exercie, we will simply use the **cdn link and put it in the src script tag**.

    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">

        <-- put the Jquery CDN link in the src section -->
        <script src="https://code.jquery.com/jquery-3.6.1.js"></script>

        <title>Film</title>
    </head>
</head>

### The body:

In the body we will put a siple div with an id of ***film***.

This is where we will inject all or data once fetched. We should be directly doing anything here from now on (but you can also add a title to your page if you want).

    <body>
        <h1>Here are some Films</h1>
        <div id="film"></div>
    </body>

## 3. Fetching the data

### Before we start:

First of, we new the open a new script tag that will be our main playground for what we are about to do.

I'd recomend puting this script tage in the head below the script where we imported jquery.

A good thing to already include in your script is the **.ready()** method that will execute what's inside only after the elemnt that comes before has been fully loaded or executed.

    <script>
        $(document).ready(function () {
            // Code goes here
        })
    </script>

### The fetching:

To start fetching from our json (or any DB you may have created) we will use jquery's **$.post()** method as show below.

    $.post("db.json", function (data) {
        // Here will go our main function
    })

As show above, the method **$.post()** will have two parameters:

* the first parameter is **string** containing the **path to our DB**, in this case **"db.json"**
* the second parameter is a **function** that will also contian a parameter here called **data**

