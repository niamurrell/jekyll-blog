---
layout:     post
title:      Daily Review
author:     Nia
tags: 		Jekyll Express SublimeText 
subtitle:  	Jekyll Blog Success & More Express
category:   daily
---

### Jekyll

Today I got my Jekyll blog up and running on GitHub Pages. Thanks to what I learned yesterday about Node and Express, I was able to figure out what was going on in the template I used ([Project Pages](https://github.com/projectpages/project-pages)) without too much issue. Basically it builds the site based on includes, layouts, and a minimal amount of html & markdown files. It uses special brackets `{%  %}`, similar to what Express looks for in ejs files `<%  %>`. Probably wouldn't have been able to get this up and running in just a few hours without understanding what those brackets do! Now all I have to do is write posts using markdown...it literally couldn't be easier.

I also had fun getting it to look pretty cool. I'm not a Photoshop expert by any means but I think it came out alright! Next I might add pagination and eventually would like to move it from GitHub Pages to my own website; there is a good [tutorial](http://jmcglone.com/guides/github-pages/) on how to do all of these things to review later.


### More Express

First I learned a way to make it so that you don't need to write `.ejs` every time you reference an ejs file: `app.set("view engine", "ejs");`. This goes in the main app.js file.

Stylesheets and script documents need to be stored in a `/public` directory in the root folder. In order for Express to look from them, you need to include the following in app.js: `app.use(express.static("public"));`. **Note:** it's very important to pay attention to the path names here, being sure to include slashes `/` where needed.

I also learned the Express way of doing Jekyll's includes & layouts. In Express they're stored in `/views/partials` in the root directory. Files like `head.ejs` and `footer.ejs` would go in this directory with all of the html needed for these sections. Likewise for Google anayltics, sidebars, etc. To include it on the page add `<% include partials/head %>` where you'd want the head section to go.

I'm guessing there is a way to make templates (like in Jekyll) so that you don't have to type the `include` statement into each and every page (hope so!), but we haven't learned that yet.

Also learned about ***Post Routes*** which are used to take data from the site user and add it to the site contents. This requires a new node package `npm install body-parser --save` which processes the user data on the server. It needs to be *required* and *used* in the main `app.js` file:

```
var bodyParser = require("body-parser");
app.use(bodyParser.urlencoded({extended: true}));
```

Then it can be used to add user inputs to the site output using a new command `res.redirect` and a `POST` route:

```
app.post("addentry", function(req, res) {
	var newEntry = req.body.newentry;
	entries.push(newEntry);
	res.redirect("/entries");
});
```


### Sublime Packages

I have gone back and forth between Atom and Sublime Text 3 as my text editor. Today I finally cracked how to install packages in Sublime--necessitated by working on `.ejs` files which have no syntax highlighting by default--and I think now I will stick with Sublime going forward...that was the one thing I could do better in Atom. In case I forget:

```
Cmd + Shift + P
type: install
Package Control: Install Package
then type the package to install
```


### Other Stuff

I can never remember what API stands for; today I was reminded it's **Application Program(ming) Interface**!!


### Up Next

Tomorrow is the 4th of July so not sure how much I'll get done. But I'd like to finishe the APIs section of my bootcamp course and then dive into databases. I've also got a pile of problems to figure out with my AWS hosting so if there's time will work on that tomorrrow.