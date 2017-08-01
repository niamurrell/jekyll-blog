---
layout:     post
title:      The Final Stretch
author:     Nia
tags: 		  Passport Authentication
subtitle:  	Daily Review
category:   daily
---

Wow!--I can't believe it's been 5 days since my last "daily" update. I guess that login thing really took a lot out of me! Not to say I haven't been coding though...we're in the last stretch for our group project, presenting in two days, so have been working away at trying to get it ready for deployment.

### Learning More About Authentication

Once I got the login functionality working on our group project, I went back to the bootcamp to keep learning--I still didn't know how to use the user's details within the site once they are logged in.

For example in our app, the user earns points by riding public transport, and then uses their points to "buy" rewards from local businesses. So obviously once they log in, they are going to want to see how many points they have!

This turned out to be relatively straightforward, thanks to Passport. As part of the authentication process, Passport creates a `user` value in the `req` (request) JSON object, which means you can call `req.user` to pull in the logged in user's details. This can be applied to all routes within the local responses by using this function at the top of the `app.js` file:
```javascript
app.use(function(req, res, next) {
  res.locals.currentUser = req.user;
  next();
})
```

So now as long as the user has logged in, they can see their name, their points, and whatever other information we want to pull from the database about them. Sweet!

We can also use this to display different navigation items depending on whether the user is logged in or not...for example if they are already logged in they don't need to see the 'Login' or 'Sign Up' buttons. So just throw a bit of ejs into the nav bar and bob's your uncle:
```html
<div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
  <ul class="nav navbar-nav navbar-right">
    <% if(!currentUser) { %>
      <li><a href="/login">Log In</a></li>
      <li><a href="/register">Sign Up</a></li>
    <% } else { %>
      <li><a href="#">Signed In As <%= currentUser.username %></a></li>
      <li><a href="/logout">Sign Out</a></li>
    <% } %>
  </ul>
</div><!-- /.navbar-collapse -->
```

### Other Stuff

Figured out how to validate a form using jQuery. Doing so reinforced some JavaScript basics--I prefer to avoid nesting functions and *"callback hell,"* but I'm learning that it's pretty much not avoidable. I had listed each of the functions in a js file expecting it to execute from top to bottom, but some code at the bottom broke the whole thing. It was necessary to put all of the functions into one function and then execute them all at the same time to get it to work. I would like to understand this better--I get why it worked but I don't fully get why the first way couldn't work.

### Up Next

Tomorrow we finish and deploy our group app!

I'm also 4ish modules away from finishing my bootcamp completely.

I don't know what I'll do with myself with so much extra time on my hands!
