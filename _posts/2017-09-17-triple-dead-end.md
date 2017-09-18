---
layout:     post
title:      Triple Dead End
author:     Nia
tags: 		  Struggling
subtitle:  	Daily Review
category:   daily
---

I hit a wall in all three of the things I'm working on right now. It's been frustrating but I kind of have a path forward, at least for one of them.

### CS50 Dead End

I know I say this with every assignment, but today I started on the latest assignment and *literally* had no idea where to begin. We are building a spellchecker in C and are given a "dictionary" (i.e. a list of 143,000 words) as well as a long text to spellcheck. We have to write a program which reads the dictionary and stores all of the words into memory using one of the data structures we learned about in the lecture (hash table, tries, etc.); then using that dictionary, we have to spell check the text. And these actions are being timed--we need to write the program to do all of this as quickly as possible.

I got as far as writing to code to open & read the dictionary...and got totally stuck at writing a function for a hash table or a trie. That was pretty frustrating and I just didn't have it in me to power through today. If I weren't so stubborn about finishing the course, today would have been the day I'd give up!

### Metro App Dead End

I also picked up the Coding For Product project again to try and get it to be a bit more presentable. Although we got it working for our final presentation at the end of the workshop, there were still a few important bits & bobs we didn't have time to implement before, which really should be addressed if it's going to be a good example of code to reference or talk about.

The first thing I wanted to work on was getting the login sessions to persist which I finally did do over the [last](https://niamurrell.github.io/daily/2017/09/13/persistent-login/) [three](https://niamurrell.github.io/daily/2017/09/14/persistent-login-codepen/) [days](https://niamurrell.github.io/daily/2017/09/15/persistent-double-header/), but in doing so, I somehow made it so that 2 login attempts are required before you can get into the app. I don't know what I'm missing and it's frustrating, after spending hours staring at the same brick wall.

I braved StackOverflow to try & get some help but haven't gotten any responses yet. I will try some Slack groups or maybe a meetup this week if I can't work it out. But for today, I'd had enough.

### Value App Dead End

I also spent several hours working on my [Value App](https://niamurrell.github.io/search/index.html#ValueApp) trying to access nested, referenced data inside a MongoDB collection. When I build the model, I followed along from another project where I was able to do the exact same thing successfully, but in this project for some reason it's not working. I think it's something to do with accessing objects vs. arrays, and how to call them using Mongoose. Anyway lots of trial & error, YouTubing, StackOverflowing and I couldn't figure it out.

So at least with this one I've determined something I could do now. I enrolled in a (yet another) Udemy course specifically focused on MongoDB and Mongoose which I'm hoping will help me build the app. Actually I think it really will, because my only experience so far is doing CRUD commands with things like blog posts or comments, but my app will be a little bit more involved and truth be told, I wouldn't know where to start on some of the features once I get past these schema design issues.

Is it bad/procrastination/the easy route/overloading my workload to add another course into the mix right now? Probably. But I don't know where to get the kind of help I need, and I'm tired of getting nothing done!

I've only just started but I think it will be good as the course uses ES6, which I don't have much practice in but want (need) to learn, and it definitely looks like we'll be covering all of the skills I need to build my app. So here's going for the best!

### Other Stuff

I'm re-listening to the book **Grit** by Angela Duckworth and this time taking notes before I return it to the library. It's a good book with some good advice to remember! I also picked up the Elon Musk biography (on sale today on Amazon) and am looking forward to reading about his backstory.

### Up Next

Speeding through the Mongo class so I'm not too delayed on completing an MVP for my value app. I also don't want to let CS50 build up as too hard in my head so will jump back into the spellchecker assignment asap.