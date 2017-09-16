---
layout:     post
title:      Persistence - 1 Down, 1 To Go
author:     Nia
tags: 		  ValueApp PostgreSQL
subtitle:  	Daily Review
category:   daily
---

I got the login sessions to persist!! Wooooo 🎉🎉🎉 !!! After all of [yesterday's research](https://niamurrell.github.io/daily/2017/09/13/persistent-login/) it only took about 5 minutes to set it up...turns out with MongoDB and the `connect-mongo` npm package it's actually pretty simple, as suspected. Big relief!

### Persisting Sessions with PostgreSQL

Next I went back to my [CFP](https://niamurrell.github.io/search/#CodingForProduct) project to try and get it working with a Postgres database with Sequelize as the ORM. Just remembering how to use the Postgres command line was tricky! It's crazy how if you don't use this stuff you really do lose it. 

Now with a bit more understanding I can also see that our code for that project is pretty all over the place! I tried to set up some database models and put a lot of code in the wrong place which made it difficult to bring sessions in, and I'm still trying to figure it out.

### Other Stuff

I went to my first [CodePen](https://blog.codepen.io/meetups/) meetup tonight hosted by [Media Temple](https://mediatemple.net/). It was great! Met some really cool people and learned more about how to get started with CSS Grid. So that project is still very much front of mind!

### Up Next

Tomorrow there's another meetup in my area and there will be "advisors" who can help on random coding issues. Hopefully I can get the sessions to persist by the time it's over.