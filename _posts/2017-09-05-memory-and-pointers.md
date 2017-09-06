---
layout:     post
title:      Memory & Pointers
author:     Nia
tags: 		  C CS50
subtitle:  	Daily Review
category:   daily
---

### Memory Intro

Started learning about memory today and when happens when a program is run: the computer allocates some memory to run the program and partitions the memory for different functions. The **stack** and **heap** are shared within the same space; in a C program the stack is at the bottom with the *main* function making up the base. On top of that, for each function called within `main`, its data is stacked (and then inner functions stacked further on top, and so on...) until the function has executed & returned (and then erased from the memory store). The **heap** is where variables and stored values are held, starting at the top and moving downwards towards the stack. Problems happen when these collide.

You can use the `malloc()` function to tell the computer to allocate a certain amount of free memory to a given variable. This makes sure you don't overwrite memory that's needed for something else. You have to pay attention to how much memory is allocated (including a bit for ending strings `\0`, etc.). You also have to `free()` the memory once you don't need it anymore, or it will cause **memory leaks**, which is a big problem in programs that aren't closed frequently (*ahem* Chrome and its billion tabs!).

### Pointers

We also learned what's beneath the `string` variables that the course helper files allowed. A `string` doesn't actually exist, rather it's a **pointer** to an address where the beginning of the string is stored in memory. When you call a `string` the computer goes to that address in memory and pulls back everything up to the end `\0` of the string. So the "string" data type we have been using is actually a `char *`, that is, an address of a character where the string starts in memory. 

Three things to remember about pointers:
* Initially pointers don't point to anything (not setting this up is a huge source of bugs!!)
* You must *dereference* a pointer to access its pointee
* Assignment `=` between pointers makes them point to the same pointee

### Other Stuff

I learned what Stack Overflow means!

### Up Next

* Watch the concept shorts to really solidify the topics from this lecture.
* Start & finish the homework assignment THIS WEEK! Keep this train rolling...