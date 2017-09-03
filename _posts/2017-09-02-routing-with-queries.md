---
layout:     post
title:      Routing With Queries
author:     Nia
tags: 		  ValueApp RESTful Express
subtitle:  	Daily Review
category:   daily
---

I did a lot of work on my [value app](https://niamurrell.github.io/search/index.html#ValueApp) today, mostly setting up the CRUD routes for the `things`. The last time I worked with it I was focusing on the login feature and was hitting some snags so today I decided to focus on the core functionality of the app: actually creating `things` and tracking their value! I can always add the login later.

### RESTful Routing with Queries

After building the basic routes, I realized I had not set up my database to allow users to share the `things`. Ultimately users will be able to see all the things they can add (ideally with predictive search), so this really needs to be its own set of data. However for each `thing` a user has claimed, they will also need to be able to edit its purchase price and all the times they used it. So the user schema needs to reference the list of `global things`, but still have its own information about each `thing`. Not sure if I'm explaining this well after a few hours staring at this...

Anyway I made this possible by having the user create a new `global thing` first (ultimately they will be able to select from all of the global things, or create a new one), which redirected to the `new` route on submitting the initial form. On the `new` form, I wanted the `thing` name from the previous form to show up as a header. First I tried `res.redirect` to the `new` form, but learned that you can't pass data through redirect routes. Then I tried `res.render` but this doesn't work either; it tried to render a non-existent page since it was coming from a `post` route.

And hence I was reacquainted with query strings! [This Q&A on StackOverflow](https://stackoverflow.com/questions/19035373/how-do-i-redirect-in-expressjs-while-passing-some-context) had a very clear explanation on passing data through routes and I added the following to my post route on the initial form:

```
var newThingName = encodeURIComponent(req.body.name);
res.redirect("/mythings/new/?name=" + newThingName);
```

On the `mythings/new` `get` route I created a variable from this query and passed it into the page:

```
var newThingName = req.query.name;
res.render("things/new", {newThingName: newThingName});
```

Success!

### Up Next

To link the `things` to a user, next up will be finishing up the user accounts and login. Then I'll have to update all the models and routes to look for the `things` inside the user profile.