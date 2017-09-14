---
layout:     post
title:      Login Sessions & Cookies
author:     Nia
tags: 		  Authentication Passport Express MongoDB ValueApp
subtitle:  	Daily Review
category:   daily
---

I took another crack at setting up persisting sessions today. This is something I haven't implemented correctly on a couple of projects now, and I really want to get it working. This way I won't have to log in again every time I restart the server while I'm building my [value app](https://niamurrell.github.io/search/index.html#ValueApp), and after deployment users won't have to keep logging in either.

### Figuring Out Sessions & Cookies

I was under the impression that it's necessary to store session data in a database which I wasn't figuring out so easily. Turns out that may not be the best path; [this article](http://nodewebapps.com/2017/06/18/how-do-nodejs-sessions-work/) helped elucidate the options, and explained that storing sessions in a database can be pretty inefficient because of how many calls you'd be making to the db. Good point!

But I kept reading and learned that with Express & Passport, storing sessions to a db seems to be the accepted norm and best practice. Why is this? I was pretty convinced by the argument above. Well [this article](https://www.airpair.com/express/posts/expressjs-and-passportjs-sessions-deep-dive) explains some errors you might make setting up your server file; fixing them results in fewer calls to your database. Also if you use only cookies, you're limited by whatever settings the user sets in their browser, which I could see might make the site stop working correctly?

If cookies *are* the preference I came across another npm package [cookie-session](https://www.npmjs.com/package/cookie-session) which stores session info in a cookie on the client side. You would use this instead of `express-session` which stores a session id in a cookie on the client side, but stores all other session info elsewhere (database, cache, memory, etc.). But further reading suggests this opens security issues, and instead it's safer to keep user info from going back and forth to the client.

So now I am back to figuring out how to store session data in my database, as an extension of `express-session`. So...back to square one! The npm package `connect-mongo` seems to be the way to go; it's maintained by the team behind MongoDB so that's promising for long-term support. More good news: because I'm using the MEAN stack for my value app (or, MEN stack actually..) there is a lot more knowledge out there on implementation since it's a popular combination. By contrast using PostgreSQL and Sequelize on one of the other apps wasn't so easy to figure out, apparently this is a much less popular combination and there's very little written about this implementation. So I'm hoping I will have success this time around!


### Up Next

Next up is to try & implement `connect-mongo` with Express & my database. I'm also due to start the CS50 homework and finish by Sunday ideally.