---
layout:     post
title:      
author:     Nia
tags: 		  
subtitle:  	Daily Review
category:   daily
---

Today some of the groups in the Coding For Product workshop got together to spend some time working on our projects. It was a long day (especially since I skipped eating lunch!) but we got a lot done! It was great to get some experience working with GitHub and another person on the same project. Up until now I've only had my own projects to very little (if any) branching and definitely no conflicts to merge.

### Splitting The Work

After we got a few things sorted out about our plan, we basically had carte blanche to work on whatever we wanted for the rest of the day. So between one of my teammates and me, we decided to split up different features to work on--she would create the sign up page for our app and I would work on styling the redeem page. It definitely made sense to work on parts of the app that were very separate...divide and conquer and all that. But at the end of the day we still had some merge conflicts to resolve!

### Merging Different WIP Branches

This took some talking through because both branches we were working on were very much works-in-progress so we were hesitant to merge into the master branch. But we each had made changes to important parts of the repo so ultimately had to merge our work into master to share our work. It was a bit nerve-wracking to fiddle with the master but it worked in the end. Here's the basic workflow of how we had success:

```
Branches: master, sign-up, redeem

*** On sign-up branch:
git add .
git commit -m "commit message"
git checkout master

*** On master branch:
git pull origin master (double check all is updated)
git checkout sign-up

*** On sign-up branch:
git merge master
git push origin sign-up
-- generate pull request, get code approved
git checkout master

*** On master branch:
git merge sign-up
git push

*** Person 2, On master branch:
git pull origin master
git checkout redeem

*** On redeem branch:
git add .
git commit -m "commit message"
git merge master
-- resolve conflicts!!!!!!!
git push origin redeem
-- generate pull request, get code approved
git checkout master

*** On master branch:
git merge redeem
git push
```

After all of these steps, we both had each other's code and the app was up to date. We haven't deleted the branches as there's still work to do on them, but eventually will get to that point. Also I included pull requests in the steps above (for my own future reference) but since we were sitting next to each other going through the code together as it was written, we actually skipped this step.


### Other Stuff

Also worked a bit more on styling our app. It's fun but frustrating! I was trying to get 3 divs aligned next to each other within a container div for the longest time and *could not get it*!!! The solution was floating the first child div to the left (it's always a float!! 😩):
```
.parent-div > div {
    float: left;
}
```

So really grateful for the mentors who volunteer their time to hang out and help with all of these kinds of questions. It makes such a difference!

One of them also told us about [Gitkraken](https://www.gitkraken.com/), a GUI for git to facilitate workflows like the one above, and also as a way to visualize branches and the commit history. I will be trying this!

### Up Next

Back to the workshop tomorrow. So much to work on but brain is tired!
