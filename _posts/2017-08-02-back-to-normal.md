---
layout:     post
title:      Back To Normal
author:     Nia
tags: 		  Express Refactoring
subtitle:  	Daily Review
category:   daily
---

Now that [Coding For Product](https://niamurrell.github.io/search/#CodingForProduct) has ended I have a lot more time but 100% less deadlines to work towards! It shows just how much I enjoyed working with a team towards a goal. Without something like this on the horizon it's less of a given to spend 2-3 hours/night working on a project, but glad to say I am still sticking with it--the code must go on!

### Refactoring

I'm carrying on with the bootcamp and today we learned about refactoring routes and functions to add a bit of structure to the app we're building. For example the `app.js` file had 160 lines of code to start, including all of the package requirements, authentication setup, and navigation routes. Some of these pieces were moved into separate files, and after refactoring the file went down to 49 lines of code. It makes it a lot easier to move around inside the files when the file structure is broken out like this, although I'm still getting used to figuring out where everything is. It's also confusing that the naming convention is for files to have the same or similar names in different folders! But I guess I'll get used to it.

To break the code out it's a matter of creating a new `.js` file and cutting and pasting the code into it. Any packages or models that are referenced in the code need to be included as variables `var` at the top of the new file. In this process we also use the Express `router` to run each route, rather than calling `app` as before. Then the router needs to be exported at the bottom of each file: `module.exports = router;`. This is probably better explained by looking through the code...[this git commit](https://github.com/niamurrell/firecamp-yelp-clone/commit/a9dca308e12826df6ac4dc408caebe91d6235489) demonstrates the changes.

Similar to the routes, we also refactored the middleware, and in doing so set up a structure to be able to easily add new middleware functions into the app in a centralized location. We saved all of the functions in a `middlewareObject` which was then required on all of the route documents.


### Other Stuff

I got my [passport-sequelize-demo](https://github.com/niamurrell/passport-sequelize-demo) mini-app deployed to Heroku today. I had tried it as a test when we were figuring out deployment for our group project, but we got that sorted before I was able to get the demo app working. Now that I've gone through the process again on my own and got it working, I think I've got a good handle on deploying to Heroku. Sweet!

### Up Next

I think I can finish out the big app project in my bootcamp by the end of this week. Then I'll have to go back and do the 2 frontend projects I skipped when I needed to get prepped for Coding For Product. But planning to keep the momentum up so that I can move onto something new!