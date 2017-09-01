---
layout:     post
title:      Search & Sort
author:     Nia
tags: 		  Algorithms CS50 ValueApp
subtitle:  	Daily Review
category:   daily
---

### Search & Sort Functions

Today I have been working on the homework for CS50, writing a binary search function, and a sorting function (so the binary search can work) in C. I probably should have started with the sort function, since that's the pre-cursor to doing a binary search, but for whatever reason I did it backwards. I wrote it as a while loop to run as long as the left and right boundaries don't cross over each other (in which case the sought value is not found, return `false`). Set the middle value `mid = (left + right) / 2` and then determine which half to search with `if` statements, updating the boundaries & middle as we go.

For the sort function it was a nested `for` loop to set the minimum value at index `0` and then check each remaining index to see if it's lower than the `min`. If so, swap the numbers at the two indices, with the lowest always stored in the leftmost index.

I'm still less partial to C and it's layout, so coded these in JavaScript on [repl.it](https://repl.it/) and then translated into C once I got them working. I thought I got the solutions right, and it even passed the initial tests, but the bigger test which checks an array of length 1000 is failing so I'll look at that more tomorrow.

### Other Stuff

Today I intended to work 90 minutes on this homework assignment so that I could dedicate a good 2 hours to my value app. 4 hours later...! Typical :P

### Up Next

I decided to build my value app with a not-optimized database structure to start, just to prototype something. I also bought a MySQL class I'd been eyeing on Udemy ($10 sale!) so that I can eventually make it better. Not sure when I will have time to start that though.