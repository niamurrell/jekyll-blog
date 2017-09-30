---
layout:     post
title:      Value App Reconsiderations
author:     Nia
tags: 		  ValueApp Git
subtitle:  	Daily Review
category:   daily
---

I finished the MongoDB course and got back to working on the Value App.

### MongoDB Course Wrap Up

Turns out this course was a big distraction. I definitely did [learn some things](https://niamurrell.github.io/daily/2017/09/18/tdd-intro/) that I'll probably be able to use in the future, but after the first section of the course it veered off into topics that literally have nothing to do with this project. On top of that, I realized after finishing the whole thing that we literally never once touched the front end in the course--again not really helpful with my project since that was the main problem I was having: figuring out how to display the data in the front end properly. Also, all of the code in the course was written in ES6 and while I'm really glad to have been exposed to this, porting all the code I already wrote to ES6 just seems like a big exercise in yak shaving at this point.

So overall, not as helpful as I first imagined. BUT, the info was good and thorough, so maybe on future more relevant projects it will be really helpful to have this to go back to.


### Back To Value App

It turns out the reason my `things` weren't displaying properly was because of one simple mis-named variable (typical!). One of the course videos spelled out pretty well how you have to pay attention to naming and referencing models in a particular way, so that actually helped me solve the issue. Great!


### Reconsiderations

For simplicity's sake, and just to get an MVP out the door, I reconsidered and re-wrote my database models for this project. Originally I was nesting `globalThings` inside of `userThings` which were nested inside of each `user`. For now I will forgo the `globalThings` (maybe will add back in later) because it's not really necessary as part of this proof of concept, and I want to see some progress. I.e. I want to use this app!


### Git Stash & Amend

Because I had already gotten pretty far on working on the `globalThings` setup and because I'm working on the master branch (bad, bad) I had to get acquainted with some new git commands to get things working properly. There was one commit with breaking changes (i.e. what prompted these reconsiderations) and I learned you can `git stash` to go back to the previous commit without committing the work in progress. When finished, you can `git stash pop` to go back to your work in progress.

So I put that work in progress on a new branch (which I should have done in the first place!), went back to the master branch, and rolled back with `git reset --hard 2746d86e` (or whatever commit). Since the remote branch already had the newer commit, it was necessary to force the upstream push with `git push -f origin master`. 

Then I removed all the code for `globalThings` in the project and committed. Of course I forgot one tiny thing not worth its own commit and learned you can `git commit --amend` (or `git commit --amend -m "Commit Message"`) to make small changes without having to do a new commit. And of course, got reminded of how to exit vim with `esc` + `: w q`. I always forget that one.


### Other Stuff

Totally unrelated but I'm reading Elon Musk's biography which is really interesting, and today watched [his presentation](https://www.youtube.com/watch?v=E4FY894HyF8) at this week's SpaceX event. Really cool to see the latest of what's in the works but totally different to watch him presenting, compared to the larger-than-life, epic, mythic person that's characterized in this book! It's like two completely different people.

### Up Next

Next in the [Value App](https://niamurrell.github.io/search/index.html#ValueApp) is getting the value calculations to work. I also decided to move forward with [CS50](https://niamurrell.github.io/search/index.html#CS50) without completing the assignment yet...I'll go back to it to finish the course but I don't want to lose any more momentum.