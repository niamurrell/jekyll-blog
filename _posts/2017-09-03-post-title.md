---
layout:     post
title:      
author:     Nia
tags: 		  ValueApp Express Passport
subtitle:  	Daily Review
category:   daily
---

### Login Working

First up today, I was glad to get the login working on my value app. When I used the `register` form to create a new user, I could see in the Mongo command line that the user had been created, but in the browser I got an error `400 Bad Request`. The error was caused by the field names I was using in the form; The npm package I'm using `passport-local` by default names the login fields `username` and `password` but instead of username, my field was named `email`. Once I changed it, it worked fine and routed correctly. It's also possible to pass in the names of the field you want `passport-local` to consider as the username & password fields [per the docs](https://github.com/jaredhanson/passport-local#available-options).


### Rethinking Data Models

Next up was changing my schema models to reference each other; ultimately I want one document of `things` any user can choose from (and add to) to bring into their own list of `things`. I got the "global things" set up fine, and was working on referencing a `globalThing` from the user schema. I haven't completely figured it out yet, *but* I did get the thing's object ID to show up on the logged in user's page, meaning it sees only the `things` belonging to that user and prints them. Now I just need it to print the actual array data instead of a random id number `8ac468230hgs08s`!!


### Other Stuff

I started on the book [Grit by Angela Duckworth] and I'm really enjoying it so far. I sometimes worry that I'm trying to do too many things at once (value app, CS50, MySQL course, Python intro, this blog, etc...for example), knowing that individually these things take a *lot* of time and attention so I need to cut the list down. And while that's still true, one piece of encouragement I took from the book was that I am still going, which is a positive sign! It definitely hasn't been all rainbows and lollipops, but it's been nearly a year now that I've really be learning in earnest, and I still have as much excitement and drive around what I'm doing (maybe more) as I did when I started so that's on the right track!

### Up Next

It's really encouraging and fun to see my app coming along that I can (literally) work on it all day. I need to make sure CS50 stays in the mix if I'm going to finish before year's end.