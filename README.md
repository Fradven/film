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
* the second parameter is a **function** that will also contian a parameter here called **data**. This data parameter is actualy the data that we are now fetching from **db.json**.

### Looping through the data

The next step is to loop through the data to extract what we want and need for our page.

There are several method for this:

#### Using for() statement

You have the classic **for()** method that loops as long as the parameters inside it are true

    for (i = 0; i < data.length; i++) {
        // the variable film here will be all the data about one film from the db.json file
        let film = data[i]
    }

Our data base here is a json file with an array of object. Thus each of the object must have an index that is auto-generated. So the first film in our db will have in index of 0, the second will be 1, etc.

Therefore to select the first object in our array we write **data[0]**, to get the second **data[1]**, etc.

The **for()** statement here will increment **"i"** as long as **"i"** is stricly smaller than the amout of object in our data and we know how many elements are in our data set thanks to the **.length** property.

By puting the **"i"** instead of a number inside the brackets of **data[]**, we will be able to fetch on by one the objects from the json file.

#### Using jquery .each() method

As we have already imported jquery, we might as well use it's tools in our project.

Jquery comes with its own simplefied version of a loop, the **.each()** method.

    $(data).each(function(index){
        // code to be execute for each elements of data
    })

The jquery method is a lot cleaner and shorter then the **for()** statement shown above.

Here we are marely selecting the data using the jquery selector **$()** and puting the **.each()** method next to it with a **function** as a parameter and inside the function a parameter that is going to be one element of our data base, here called **index**.

In the method here, the loop is done for you and there are no **"i"** pass down in any brackets. It was alredy done for you!

    Note: In here the "index" parameter is equivalent to the variable "film" in the exmple for the "for()" statement. You can therefore call this parameter whatever is more appropriate.

#### Using forEach() or .map()

Javascript also come with an equivalent to the **.each()** method.

Both the **forEach()** and **.map()** method accomplish the same thing as the jquery method.

    data.forEach(function(film) {
        // code to be execute here for each elements of data
    })

    // or

    data.map(film => {
        // code to be execute here for each elements of data
    })

These methods are very similar to the jquery one by a native to javascript and do not require the **$()**.

In essence, they work the same way.

## 4. Inject the data into the page