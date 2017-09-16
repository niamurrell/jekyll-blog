---
layout:     post
title:      Persistence - Double Header
author:     Nia
tags: 		  PostgreSQL CodingForProduct Express Passport
subtitle:  	Daily Review
category:   daily
---

Two days in a row, success! 🎉🎉🎉🎉🎉🎉 Now when a user logs into the site and the server is restarted, they are still logged in afterwards. 

### Refactoring Mess

I got help figuring out the issues at a Meetup event tonight...it was so useful! When I left off yesterday, I could see that the user session was indeed being created and stored in the database (good), but for some reason when they log in it would redirect them back to the login page rather than going to the user's dashboard (bad).

The person who helped me showed me a bit more of the Chrome developer tools I hadn't seen before. With this we were able to see that it *was* going to the dashboard, just quickly routing again back to login. Hmmm. 

Then we rolled back to the last version that allowed the login to work, and did the refactor again step by step. The key thing was testing that it still worked after every change. For some silly reason I didn't do that yesterday when I moved and changed all the code around! Rookie move, that's for sure. Going through step by step I was able to find the one section of code that was breaking the whole thing. Not surprisingly it was a section I didn't fully understand, other than it was what the package docs said to do.

Eventually I figured out that some of the options were configured for an HTTPS environment, and when I adjusted them it started working. So now it's completely working as it should!

### Well, almost...

There's now a weird thing happening where it takes two attempts to log into the site. Even worse, if you try one user on the first attempt and a different user on the second attempt, it logs you in as the first user! Pretty critical error, so that's what I'll be working on next.

### Up Next

I'll also need to put this aside eventually to finish the CS50 assignment this weekend.