---
layout:     post
title:      Express-less Node.js Server Part 2
author:     Nia
tags: 		  Node JavaScript VSCode
subtitle:  	Daily Review
category:   daily
---

### Creating & Routing A Node Server ...continued

Today I picked up where I left off [yesterday](https://niamurrell.github.io/daily/2017/12/09/expressless-server/), and got the query from the URL parameters to persist as a JSON object. I learned about the [`Object.assign()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) method which does the trick. After creating an empty object as a global variable (`var db = {}`), you can assign data to a target: `Object.assign(target, data)`. So for this server I added this into the routing logic to produce the desired result:
```javascript
// Handle routes
  if (pathname === "/set") { // SET sends params to JSON object
    db = Object.assign(db, query);
    resMessage = "You have stored " + JSON.stringify(query) + " in memory.";
    console.log(db);
  } else if (pathname === "/get") { // GET finds params from JSON object
    var key = query.key;
    var value = db[key];
    resMessage = "The value of '" + key + "' is: " + value;
  }
```

So that's the challenge done! The full code is in this [gist](https://gist.github.com/niamurrell/87d8b7e120491c52f75f08acde2c7b5f). 

### Other Stuff

I spent a good 20 minutes trying to figure out how to take Git Code Lens annotations out of the editor in VS Code. For future reference: `shift` + `alt` + `b`!!!!


### Up Next

Deploy my [value app](https://niamurrell.github.io/search/index.html#ValueApp) without the delete function. Hoping I can get that working at some meetups this week, but I'm overdue in trying to deploy on AWS so I will do that first.