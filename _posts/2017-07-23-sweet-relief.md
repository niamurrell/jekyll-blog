---
layout:     post
title:      Sweet Relief!
author:     Nia
tags: 		  Passport Mongoose Sequelize CodingForProduct RESTful Databases
subtitle:  	Daily Review
category:   daily
---

It's working! Words can't event describe the sweet relief of getting our login function working. Well, they probably can, but I don't have the words, because my brain is mush.

### Slow & Steady Wins The Race

This week I skimmed the book [Think Like A Programmer](https://www.goodreads.com/book/show/18469872-think-like-a-programmer) by V. Anton Spraul and it was a big catalyst for solving [all](https://niamurrell.github.io/daily/2017/07/16/workshop-day/) [of](https://niamurrell.github.io/daily/2017/07/18/login-delays/) [the](https://niamurrell.github.io/daily/2017/07/19/sloggin-login/) [login](https://niamurrell.github.io/daily/2017/07/20/daily-review/) [issues](https://niamurrell.github.io/daily/2017/07/22/slowly-making-progress/) of this week. For troublesome problems he advised writing test programs only for the feature you're trying to implement...once you can do it on its own, it will probably be easier to make it work in the bigger project. I had been pecking around with aimless trial & error for hours over days so literally had nothing left to lose.

#### Passport / Mongoose Demo App

As luck would have it, the online bootcamp I'm doing alongside the group project has a module on creating a test login app, so I started with this. That class is using MongoDB so it's not exactly like-for-like but I got it working. Working with MongoDB and Mongoose was easy compared to PostgreSQL/Sequelize, and made even easier by the `passport-local-mongoose` package which handled the password hashing and some of the authentication methods. My repo of the demo is [here](https://github.com/niamurrell/passport-mongoose-demo).

#### Passport / Sequelize Demo App

Next I attempted to translate the mongoose demo to work with Sequelize. It became clear pretty quickly why our app has been so difficult to work with! By comparison Postgres/Sequelize needs a lot more code and attention than MongoDB/Mongoose...comparing the `models/user.js` files in the two demos shows just how much. Not to mention futzing around Terminal in the postgres CLI.

The ease of the `passport-local-mongoose` package made me look for a Sequelize equivalent and I soon came across `passport-local-sequelize` which is meant to have the same functionality. The documentation wasn't as robust and the adoption was significantly lower, but I figured I'd just need to figure it out. The implementation was a bit different but in the end I got this demo working as well ([see repo](https://github.com/niamurrell/passport-sequelize-demo)).

#### Integration With Our App

With a working example to compare against I got working on our app. There was a lot of messy code to clear out following all of the trial & error that went on earlier. But a quick clean out, destroying then rebuilding the user database from scratch, and then re-applying what I picked up in the demos, and **SUCCESS**! Now we can create a new user with the sign up form, log them in and out, and protect the inner pages from unauthenticated users.

#### Resources

I came across several good references from other people working through the same issues. These will probably come in handy for the next steps in the process:
* [mgritts progress blog post](http://mgritts.github.io/2016/08/30/cp5-sequelize-up-running/) - implementing RESTful routes with Passport & Sequelize
* Lynda Chiwetelu's [detailed article](https://code.tutsplus.com/tutorials/using-passport-with-sequelize-and-mysql--cms-27537) on implementing Passport with Sequelize (but with MySQL not PostgreSQL)
* [Raymond Camden's troubleshooting tips](https://www.raymondcamden.com/2016/06/23/some-quick-tips-for-passport/) for using Passport
* toon.io's overview of [authentication flow](http://toon.io/understanding-passportjs-authentication-flow/) for the bigger picture, to keep things on track
* Chris Courses YouTube series ([video 1](https://youtu.be/gYjHDMPrkWU)) on implementing authentication with Passport, *very* well taught (but with MySQL and MAMP)
* Wai-Yin's start-to-finish overview for Coding For Product ([demo](https://www.youtube.com/watch?v=Iu2bIg8fvTw) and [code](https://github.com/CodingForProduct/demo-express-lowdb-passport)), again for bigger picture (but with Lowdb)


### Other Stuff

After going through the demos I put together a table of the RESTful routes and how to call user data for each route, whether you're using Mongoose or Sequelize. [The gist is here](https://gist.github.com/niamurrell/eb80dff74e6af2d93a2283f275a267bc) and I'll probably update this if/when I need to use yet another ORM in a future project.

### Up Next

While the login feature is working (huzzah!) I still need to add in session handling so that the login state persists. It also still needs error handling so that the user is told what went wrong if an error happens. Fingers crossed these are easier to figure out!
