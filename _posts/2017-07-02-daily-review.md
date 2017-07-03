---
layout:     post
title:      Daily Review
author:     Nia
tags: 		JavaScript Node Express Tools
subtitle:  	Jumping Into The Backend
category:   daily
---

I have been working on a [Udemy web development bootcamp](https://www.udemy.com/the-web-developer-bootcamp/) for about a month now. It started with front-end development: HTML, CSS, Javascript, and jQuery. Yesterday and today has been jumping into the backend, first getting set up with Node and then the Express framework. 

### Node.js

A few weeks ago I went to an "intro" event where I was hoping to get a basic understanding of Node.js but at that time I barely understood how the backend even works so it mostly went over my head. Now it's been explained really well in my bootcamp so I actually understand what it's for and how to use it!

The first Node exercises were similar to the first exercises that we did in the JavaScript modules, only run on the server instead of the browser. 

We also used a few npm packages to see their usefulness and how to install them. A good one for generating fake data was [faker](https://www.npmjs.com/package/faker) ⭐️; it can generate a lot of real-looking information like names, product names, addresses, databases, images, etc. That will be really useful in the future when mocking up sites and apps.

### Express

Express is a popular web app framework written with JavaScript. They chose Express for the course because a) it's popular (and therefore lots of tutorials, community, etc. to learn from or get help from) and b) because it's considered a 'lightweight framework,' meaning you really have to understand how it works in order to get it to do things. This is in contrast to a 'heavyweight framework' which does a lot of the work for you...good because it's easier, but you might not understand as much about how things work.

To create an app using Express we:
* Open Terminal and go to `cd` (or make `mkdir`) the directory where we'll build the app

* Make an app file: `touch app.js`

* `npm init` to create the `package.json` file. It will go through a few steps...make sure the entry point is `app.js`.

* Require Express in the `app.js` file at the top:

```
var express = require("express");
var app = express();
```

* Include ***routes*** to tell the app what to do (more below).

* Tell the server to listen for routes at the bottom of the `app.js` file (the function is optional but helpful):

```
app.listen(3000, function() {
	console.log("Server has started on Port 3000.");
});
```

### Routes

This is like the big cahuna of getting it all to work. Routes are what tells the app what to do when each page is called, what dynamic information to change on the rendered site, and I have a feeling a lot more that I'll learn in the future! These are the main bits of code I want to remember:

```
app.get("/", function(request, response) {
	response.send("Hello world!");
});
```

Conventionally `request` and `response` are often shortened to `req` and `res`. Both are very important: `req` is an object that contains all of the information about what triggered the route and `res` is everything you'll send back to be processed or rendered by the server.

```
app.get("*", function(req, res) {
	res.send("This page doesn't exist...sorry!");
});
```

You can use a catch-all route to control the message for pages that don't exist. This must be below all of the other routes to work properly (otherwise all pages will get this response).

```
app.get("/blog/:month", function(req, res) {
	var month = req.params.month;
	res.send("The month is " + month + "!!");
});
```

**Route parameters** are identified using the colon `:`. This tells Express to look for a pattern instead of a specific path. You have to include the full path in your route, for example if the path in your route is `/blog/:month/:day` and you instead go to `/blog/january/1/title-of-my-post` it will not be found since there is no 'title' to look for in the pattern.

`params` is one of the many key-value pairs in the `req` object, this is how you create a variable from the path name.

And important to note: `res.send` will only send once so you need to include everything to be sent in a single command. If looping through information, you would first need to collect everything into a variable, and then `res.send` the variable; you can't include `res.send` within a for loop as it will just stop!

### Express + ejs

You can tell the app to render a page using `res.render()`, but rather than rendering .html files, Express uses ***Embedded JavaScript (ejs)***. Ejs is an npm package which must be installed to the app directory from Terminal using `npm install ejs --save`. Then Express will be able to look for your html (ejs) files in the `/views` directory, which is created during the install. Here are the bits of code I want to remember for using ejs:

**Make dynamic fields in an ejs file:**

In the ejs file:
```
<h1> Welcome, <%= name %> </h1>
```

In the app.js file:
```
app.get("/:userName", function(req, res) {
	var userName = req.params.userName;
	res.render("app.js", {name: userName});
});
```

This will render the user's name in the H1 on their client.

**Use conditional rendering in an ejs file:**

```
<h1> Welcome, <%= name %> </h1>
<% if(name.toLowerCase() === "nia") { %>
	<h2>This is your website!</h2>
<% } else { %>
	<h2>Thanks for visiting!</h2>
<% } %>
```

These special brackets `<%=  %>` and `<%  %>` must surround every line of embedded JavaScript in the code. If you use the equals `=` sign it will evaluate the js within the brackets, so when using conditional statements you have to use the brackets without the equals `=` sign.

**Using a loop to render multiple objects in an ejs file:**

In the app.js file:
```
app.get("/posts", function(req, res) {
	var posts = [
		{title: "Post 1", author: "Nia"},
		{title: "Post 2", author: "Jennifer"},
		{title: "Guess", author: "your mom"}
	];
	res.render("posts.ejs", {posts: posts});
});
```

In the posts.ejs file:
```
<h1>The Posts Page</h1>
<% posts.forEach(function(post) { %>
	<li>
		<%= post.title %> - <%=post.author %>
	</li>
<% }); %>
```

You could get the same result using a for loop:
```
<h1>The Posts Page</h1>
<% for(var i = 0; i < posts.length; i++) { %>
	<li>
		<%= posts[i].title %> - <% posts[i].author %>
	</li>
<% } %>
```

The resulting list would be:

**The Posts Page**
* Post 1 - Nia
* Post 2 - Jennifer
* Guess - your mom

### Other Stuff

We had our second day of **[Coding For Product](http://codingforproduct.com/)** workshops today. We learned about:
* Writing readable code
  * use linters like eslint to check for errors and style
  * use descriptive variable and function names
  * DRY (don't repeat yourself)
  * include instructions on how to get started with the app in your README file
* Debugging
  * read error messages to see where the error is, even if the error message itself doesn't make sense
  * `console.log` variable values throughout to see what's happening
  * use Chrome developer tool to run through code step-by-step
* Using front-end design frameworks like [Bootstrap](http://getbootstrap.com/), [Foundation](http://foundation.zurb.com/), [Bourbon](http://bourbon.io/)
* Databases
  * relational vs. NOSQL
  * CRUD commands in SQL
  * using an ORM library to query & update databases
  * using migrations to update the database schema

Also at the end of the class one of my teammates told me about these easy, awesome Jekyll blogs, so I created this! It's built on Ruby so I guess I'll be learning a bit of that.

### Up Next

Tomorrow I'll keep going with the bootcamp and will go a bit deeper into databases. Looks like we'll be using [MongoDB](https://www.mongodb.com/) so totally different to the workshop today.

I also have to reseach sign-in and authentication for our Coding For Product app. No idea where to start there so it will be interesting!



