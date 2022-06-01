# Challenge: A Quote Server

## How long will this take?

- 1 hour (level 1)
- 3-4 hours (advanced level)

## Overview: what is this challenge?

In this challenge you have to create a server (using Node and Express) which serves quotes, in JSON format.

In the _extended_ work of this challenge, you also make a React app which displays the quotes retrieved from your new server.

Here's how it might look if you make a request to such a server.
![screenshot of the server in use](./screenshots/quote-server-example.png)

## Getting Started

Fork this repository and read this file. This document outlines all of this tasks to complete this weeks homework.

## Want to run your code on the internet?

- Open Postman app
- run `npm install` and `npm start` in your folder
- use `http://localhost:5000` as URL in the Postman

## Level 1 Challenge - make the quote server

Your server must have at least these two "routes":

- `/quotes` - returns ALL of the quotes, as JSON.
- `/quotes/random` - returns ONE of the quotes, picked differently at random each time it is requested.

A list of quotes (in JSON format) is provided in this repo [quotes.json](./quotes.json). Each quote is a simple object with a quote and an author.

Try to use what you know to do this challenge on your own. However, there are some steps to guide you, below.

## Add a `/quotes` route

Add a `/quotes` route to return _all_ of the quotes as JSON.

Note that the quotes have already been loaded for you from a JSON file.

Test that your server successfully serves all of the quotes as json on Postman by making a request for /quotes from your new server.

### Help - how do I add a route?

To add a new route, you can copy-paste an existing route and change its parameters.

For example, here are two (very boring) routes

```
app.get('/one', function(request, response) {
  response.send("You asked for route /one")
});

app.get('/two', function(request, response) {
  response.send("You asked for route /two")
});
```

You can refer to this short [Basic Routing](https://expressjs.com/en/starter/basic-routing.html) document for discussion on what each part does.

## Add a `/quotes/random` route

Add a `/quotes/random` route to return _ONE_ of the quotes, picked randomly on each request.

The JavaScript to pick randomly from an array is actually quite difficult, so we've provided a function to help you, called `pickFromArray`.

If you want a tougher JS challenge, feel free to write your own function which returns one element at random from any given array, and use that!

Test that this route is working too by making a request to `/quotes/random` You should get one quote - an object with a quote and an author.

Be sure to check that the previous routes `/quotes` and `/` are still working, too!

## End of Level 1 challenge!

Well done!

- Push your working server on your Github account
- Read the following ideas for further work

## Level 2 Challenge - respond from url with _parameter_!

### Overview

In this exercise the user will send data through the url.

When the user changes the url like this:

- `/quotes/search?term=life`
- `/quotes/search?term= `
- `/quotes/search?term=miss`

The server will respond with `life`, `success`, `miss`

Extra (bonus) requirements:

- bonus: make your search case-insensitive
- bonus: make the search return matches on quote OR author text.

### Go ahead!

If you think you know how to do that, go ahead!

#### Algorithm

1. receive a term from the URL
2. make the server respond with it

For this exercise only an endpoint is needed.

#### Getting parameter(s) from the URL

We have to learn how to get the search term from the user. This is very easy to program, but you should read on to understand what is going on.

Users of the API will add their search term to their URL with a _query parameter_ called `term`.

So, for example, if the user wanted to print the word `life` , their HTTP request might be: `/quotes/search?term=life`

You should [read about the query string part of the URL, here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Identifying_resources_on_the_Web).

#### So, how do I get these query parameters when using Express?

In express, we use the object `req.query`, to which we have to include the name of the parameter we used `.term`, it will have all the parameters passed to us in the URL's query string. [The official documentation is here](https://expressjs.com/en/api.html#req.query).

To use it we need to declare it as a variable.

#### An intermediate step, use of the _parameter_

After learning how to declare and use the parameter we are gonna use it to search specific quotes from the JSON.

It should work with requests like this one:

- `/quotes/search?term=life`

The algorithm should:

1. receive a search term (a string) to look for
2. then find any quotes that contain that string in their quote text
3. then return only those matching quotes

As with `/quotes`, your new route should return a JSON array of quotes. If you find none that match, it should return an empty array, `[]`.

Remember that each quote is a `property` of each object of the array
```
[
  {
    "quote": "Life isn’t about getting and having, it’s about giving and being.",
    "author": "Kevin Kruse"
  }
]
```

### Searching for quotes - a pure JS exercise

Once you know which word you are searching for, the next task is really a pure javascript task.

Searching through your list of quotes to find ones whose text includes that word... this is done no differently in Express or Node than in pure javascript.

So I suggest you first get it working in pure javascript. That will give you less to think about.

[Here is an example pure-javascript project for developing this part of your code](https://repl.it/@enz0/findMatchingQuotes). But you could do the same in your local development environment.

Once you've got that working, you can copy-paste your function into your Express app and use it.

## End of Level 2 challenge!

Well done!

- Push your working server to your Github

### Ideas for further work

- Use YOUR favourite quotes

- Use the same code to serve something other than quotes - maybe revision notes, proverbs, or other data that you want to be reminded about.

## Challenge: Intermediate: Use a library to make random picking easier

In the real world, many developers would use a library like [lodash](https://lodash.com/) to make it simpler to do tasks like picking randomly from an array.

In this extra challenge, you should install and use lodash to do the picking.

[Here's the documentation for its sample() function](https://lodash.com/docs/4.17.11#sample).

Install the lodash library:

- edit the file `package.json`...
- add a line for lodash in the dependencies (you'll already see one for "express").
- You can use "\*" as the version number for now.
- Glitch will automatically install it.

Add a "require" line in your server.js so that you can use the library.

`const lodash = require('lodash');`

then you can use...

`lodash.sample(myArray)`

This is the same process for almost ANY library you can find on [https://www.npmjs.com/](npm).

## Challenge: Advanced: Add a React app as a front-end

Note: only do this if you have done all other Node homework this week - that is the priority.

- Make a very simple React app called quotes-react-app
- Have it fetch a random quote from your server on glitch. You'll have to enable CORS on the express app. See below.
- (Bonus: Allow the user to get a new random quote from the server, by clicking a button or clicking the quote.)
- Host your react app on netlify
- Post the URL to your hosted React app on Slack, and in your google classroom submission (along with your glitch server url)

### Example screenshot of Simple React app

Here's an example of how your react app might look.
Note I didn't add a "get new quote" button here.
![Example Screenshot of React App](./screenshots/example_react_quotes_app.png)

#### Enabling CORS on the Express app

You'll have to install and enable CORS on your server in order to allow your JSON to be loaded from a different server than your React app has been loaded from.

in `package.json` add a dependency for `"cors": "^2.8.5"`

Then in your `server.js` add...

`const cors = require('cors')`

and

`app.use(cors())`

Read more about CORS in Express [here](https://expressjs.com/en/resources/middleware/cors.html).

