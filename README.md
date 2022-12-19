# Pulling data from a DB and create a web page using Jquery

## Aim of the exercice

Simulate fetching data about movies from a data base that will be displayed on a page using jquery fetch function et loops with a button to display and hide information.

###

## 1. Create a Data Base

To fetch something, first we must have data. For that we will create a json file that will act as our data base.

We will fill the json file with an id, the title of a movie, the genre, the year it came out, the movie poster and we will create an array that will contain some characters and the name of the actors who played them.

    {
        "id": 1,
        "title": "Alien",
        "type": "science-fiction/horror",
        "release_year": "1979",
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

In this exercie, we will simply use the **cdn link and put it in the src of the script tag**.

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

A good thing to already include in your script is the [.ready()](https://api.jquery.com/ready/) method that will execute what's inside only after the elemnt that comes before has been fully loaded or executed.

    <script>
        $(document).ready(function () {
            // Code goes here
        })
    </script>

### The fetching:

To start fetching from our json (or any DB you may have created) we will use either jquery's [$.post()](https://api.jquery.com/jQuery.post/#jQuery-post-url-data-success-dataType) or [.get()](https://api.jquery.com/jQuery.get/#jQuery-get-url-data-success-dataType)  method as show below.

    $.get("db.json", function (data) {
        // Here will go our main function
    })

As show above, the method **$.get()** will have two parameters:

* the first parameter is **string** containing the **path to our DB**, in this case **"db.json"**
* the second parameter is a **function** that will also contian a parameter here called **data**. This data parameter is actualy the data that we are now fetching from **db.json**.

### Looping through the data

The next step is to loop through the data to extract what we want and need for our page.

There are several method for this:

### Using for() statement

You have the classic [for()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for) statement that loops as long as the parameters inside it are true

    for (i = 0; i < data.length; i++) {
        // the variable film here will be all the data about one film from the db.json file
        let film = data[i]
    }

Our data base here is a json file with an array of object. Thus each of the object must have an index that is auto-generated. So the first film in our db will have in index of 0, the second will be 1, etc.

Therefore to select the first object in our array we write **data[0]**, to get the second **data[1]**, etc.

The **for()** statement here will increment **"i"** as long as **"i"** is stricly smaller than the amout of object in our data and we know how many elements are in our data set thanks to the **.length** property.

By puting the **"i"** instead of a number inside the brackets of **data[]**, we will be able to fetch on by one the objects from the json file.

### Using jquery .each() method

As we have already imported jquery, we might as well use it's tools in our project.

Jquery comes with its own simplefied version of a loop, the [.each()](https://api.jquery.com/each/#each-function) method.

    $(data).each(function(index){
        // code to be execute for each elements of data
    })

The jquery method is a lot cleaner and shorter then the **for()** statement shown above.

Here we are marely selecting the data using the jquery selector **$()** and puting the **.each()** method next to it with a **function** as a parameter and inside the function a parameter that is going to be one element of our data base, here called **index**.

In the method here, the loop is done for you and there are no **"i"** pass down in any brackets. It was alredy done for you!

Note: In here the "index" parameter is equivalent to the variable "film" in the exmple for the "for()" statement. You can therefore call this parameter whatever is more appropriate.

### Using forEach() or .map()

Javascript also come with an equivalent to the **.each()** method.

Both the [forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) and [.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) method accomplish the same thing as the jquery method.

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

Now that we can extract data from the data base, we have to put in on our webpage. For that we will use [.append()](https://api.jquery.com/append/#append-content-content) to inject element into the page.

    data.map(film => {
                    $("#film").append(`
                    <div class="film-container">
                        <h2>${film.title} (${film.release_year})</h2>
                        <div>${film.type}</div>
                        <div class="poster"><img src=${film.poster} alt="${film.title}"></div>
                        <div class="character-container${film.id}"></div>
                        <button class="casting${film.id}" value="view">View Casting</button>
                    </div>
                    `)
                })

As you can see, using **.append()** we can write html tags as strings that will be create on the page. 

Here we are selecting the div we created at the beggining with the id **film** like this **$(#film)** and then we add the **.append()** method that will contain a string. Here we contain the string inside backticks ` `` ` so that we can use [template literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals).

As we know, the parameter **film** is an object. We can therefore get the element we want from it by writing **film** followed by a **dot** and then the **name of the element**

    exemple: film.title

Inside those tags,  we are suing the template literal that alows us to call script element inside a string, in this case it will be the elemnt inside the object that we want to show on the page.

Since our json has an other array inside of it for the characters that plays in our film, we must do an other loop to get those element and append them inside that loop. 

So we are doing a loop inside a loop.

    data.map(film => {
                    $("#film").append(`
                    <div class="film-container">
                        <h2>${film.title} (${film.release_year})</h2>
                        <div>${film.type}</div>
                        <div class="poster"><img src=${film.poster} alt="${film.title}"></div>
                        <div class="character-container${film.id}"></div>
                    </div>
                    `)

                    film.acteur.map(actor => {
                        $(".character-container" + film.id).append(`
                        <div class="character${film.id}">${actor.actor} as ${actor.character}</div>
                        `)
                    })
                })

As you may have noticed we **added the object's id to the class of the div**. 

The reason is that, in the first loop, we will create several time the same div and if we want to inject the element from the second loop into it we will inject it in all the div that has the same class name.

To prevent that, we added the the id of the object to the class name so that it can become unique and the second loop will only append it's information inside that one we want.

## 5. View and Close button

We now want to be able to show or hide the list of characters for each movies. For that we must create a button that will be execute on click and show or hide the content as well changing the button itself.

For that we will use several jquery method and a if()...else statement:

### Add button

First of, we need to add the button. We will put it at the end of the first **.append()** of our loop since it's a button that needs to appear for each of our movies.

Inside the button we will create a class that must include the a unique element of the object of the film for the same reason as we mentioned for appending the characters (it is recommended to use the id as it should always be unique) and we will create a value here we will call it view.

Between de tags we will write View Characters.

It should like something like this:

    $("#film").append(`
                    <div class="film-container">
                        <h2>${film.title} (${film.release_year})</h2>
                        <div>${film.type}</div>
                        <div class="poster"><img src=${film.poster} alt="${film.title}"></div>
                        <div class="character-container${film.id}"></div>
                        <button class="button-character${film.id}" value="view">View Charcters</button>
                    </div>
                    `)

### Using .on() method

Now, we must add an event listener that will ***listen*** to the button. For that we will use  the jquery [.on()](https://api.jquery.com/one/#one-events-data-handler) method and instruct it to wait for a click to activite.

    $(".characters" + film.id).on("click", function(){
        // add event here
    })

In this method, the first parameter will be that action that the method has to listen to and the second parameter will be the function that will be executed. 

There are several thing we will have to do in this function for our exercise.

### Changing the button with .val() and .html()

We will first start by changing the value and the text between the tags of our button.

For that we have the [.val()](https://api.jquery.com/val/#val) method that will take the value of what comes before, here the value will be **$(this)** which will select the specific value of the button we clicked and not other.

Now in a **if()...else** statement we will check the value of the button and depending on what it is we will change both it's value using **.val()** and it's content using **.html**

    $(".button-character" + film.id).on("click", function () {
                        if ($(this).val() === "view"){
                            $(this).html("Close")
                            $(this).val("close")
                        }
                        else {
                            $(this).html("View Characters")
                            $(this).val("view")
                        }
                    })

To summaryse, what is put inside de parentesis of the **.val()** will replace the value of the element and what is inside the [.html()](https://api.jquery.com/html/#html) method will replace what is inside the tags.

### After .append() we .remove()

The button is now ready to show the character list when we click on it and hide it when we click it again.

For that we simple append the character in our first if statement and in the else statement we select the div and add the method [.remove()](https://api.jquery.com/remove/#remove-selector)

The whole script is now finished and should look something like this:

    $(document).ready(function () {
            $.get("./db.json", function (data) {
                data.map(film => {
                    $("#film").append(`
                    <div class="film-container">
                        <h2>${film.title} (${film.release_year})</h2>
                        <div>${film.type}</div>
                        <div class="poster"><img src=${film.poster} alt="${film.title}"></div>
                        <div class="character-container${film.id}"></div>
                        <button class="button-character${film.id}" value="view">View Charcters</button>
                    </div>
                    `)
                    $(".button-character"+film.id).on("click", function () {
                        if ($(this).val() === "view"){
                            film.character.map(character => {
                                $(".character-container"+film.id).append(`
                                <div class="character${film.id}">${character.character} (${character.actor})</div>
                                `)
                            })
                            $(this).html("Close")
                            $(this).val("close")
                        }
                        else {
                            $(".character"+film.id).remove()
                            $(this).html("View Characters")
                            $(this).val("view")
                        }
                    })
                })
            })
        })
