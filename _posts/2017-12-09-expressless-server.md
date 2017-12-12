---
layout:     post
title:      Express-less Node.js Server Part 1
author:     Nia
tags: 		  Node JavaScript
subtitle:  	Daily Review
category:   daily
---

I'm learning how to write a server in Node without using any frameworks. It's a coding challenge that I want to try completing without using Express, so back into the learning curve! So far I've learned that [Express](https://expressjs.com/) is awesome. 😝

### Creating & Routing A Node Server

Node has several built-in modules which are needed to create a server and routing: 
* `http`, which actually creates the server using the `createServer()` method, and then determines the port the server will be running on using the `listen()` method
* `url`, which uses the `parse()` method to allow you to create routes so that the server responds with different actions, depending on what URL you visit. 

For now I'm just getting it to respond with plain text but you can also serve html files, video, audio, JSON, etc etc.

For this challenge I'm trying to set up a server which will store key-value pairs in memory based on the URL parameters. I haven't even gotten to dealing with URL parameters yet, or to creating the streams to store this data. For now I've been able to get the routing working, and my server can handle the routes I need with or without a search query:

```javascript
var http = require("http");
var url = require("url");

var handleRequest = function(req, res) {
  res.writeHead(200, {"Content-Type": "text/plain"});
  var parsedUrl = url.parse(req.url, true);
  var pathname = parsedUrl.pathname;

	// Routing
  if (pathname === "/set") {
    res.end("You hit the set route!");
  } else if (pathname === "/get") {
    res.end("You hit the get route!");
  } else {
    res.end("Proper URL usage: '/set?somekey=somevalue' OR '/get?key=somekey'");
  }
}

// Create & start server
http.createServer(handleRequest).listen(4000);
console.log("App running on port 4000");
```

Originally I was using `req.url` in the `if` statements, which would be fine if I weren't using query strings. But because the queries should be different each time, this didn't really do the trick, so pulling out the `pathname` from the parsed URL object was the simplest solution I could find for this.
