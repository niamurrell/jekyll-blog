---
layout:     post
title:      Node API Request & UI Mockup
author:     Nia
tags: 		  JavaScript Node Express APIs Terminal
subtitle:  	Daily Review
category:   daily
---

Happy 4th of July! To be honest it's not a holiday I really celebrated living in the UK the last 5 years but I'm happy for the day off--more study time!


### API Requests Using Node

Finished this topic in my bootcamp course which I started yesterday. Here are the main bits to remember:

***Request*** is a node package which makes http requests, and can be used to call APIs:
```
npm install request --save
```

In the app.js file it needs to be required at the top, and then you can use a request function to call the API. This function returns a string (rather than the JSON or XML needed) so you also have to use the JavaScript built-in `parse()` function to get the right output. Then you can access the data you want by following the JSON object nesting pattern:
```
var request = require("request");

request("http://formatted.api.url", function(error, response, body) {
	if(!error && response.statusCode == 200) {
		var parsedData = JSON.parse(body);
		console.log(parsedData["level1"]["level2"]["level3"]["dataIwant"]);
	}
});

You can also send the data to a page instead of just logging it to the console. To do that replace the `console.log()` function with:
```
res.render("results", {data: data});
```

To pull in search terms from the user and plug these into the API's request URL, you can use `req.query.search` where `search` is the name of the form element the user saw:
```
<form action="/results" method="GET">
	<input type="text" name="search" placeholder="search term">
	<input type="submit" name="submit">
</form>
```

Then include this term in the `GET` route that calls the API. The final route would then be:
```
app.get("/results", function(req, res) {
	var searchTerm = req.query.search;
	var concatUrl = "http://www.apiSource.com/?search=" + searchTerm;
	request(concatUrl, function(error, response, body) {
		if(!error && response.statusCode == 200) {
			var data = JSON.parse(body);
			res.render("results", {data: data});
		}
	});
});
```

Whew! Took a lot to get to this one after what I'm sure were some tiny typos which broke everything. Eventually got it running though!


### Coding For Product, Coding Begins!

I am doing a workshop where I'm in a group of 3, building a fully-functional app from scratch in 5 weeks. Today I spent a lot of time doing an initial mockup of our UI. Lots of work on that and now I'm exhausted so will write more about the project another day!


### Other Stuff

Awesome thing I learned: how to install multiple node packages at once from Terminal:
```
npm install --save express ejs request body-parser
```

Another awesome package I discovered (by necessity!!) is `nodemon` which keeps the server running and watches for changes. Saves a lot of quitting and restarting the server, especially when building a UI! It's a global package (so only install once with `npm install -g nodemon`) and then in the terminal you can run `nodemon app.js` instead of `node app.js` to start it.

I will be using both of these a lot!!


### Up Next

I still have several pages to mock up for our group project's UI and that will be the priority since we present our progress every week.

In the bootcamp I briefly started databases but need to figure out the MongoDB local installation before I can go much further.

And still need to sort out my AWS mess.
