---
layout:     post
title:      Database Planning - Store vs. Calculate
author:     Nia
tags: 		  
subtitle:  	Daily Review
category:   daily
---

I've been working on the calculations for the [value app](https://niamurrell.github.io/search/#ValueApp) and the question came up--should I store the current value of each thing and then query that item for displaying on the front end, or should I calculate the value whenever it needs to be displayed?

My original thought was to calculate it each time by dividing the original purchase price by the number of uses (stored as a [virtual type](https://niamurrell.github.io/daily/2017/09/19/virtual-types/)). I figured there must be a convention around these things and I discovered [database normalization](http://searchsqlserver.techtarget.com/definition/normalization) which actually recommends against storing calculated values in a relational database to reduce redundancy (among other reasons). However [this Q&A](https://dba.stackexchange.com/questions/239/storing-vs-calculating-aggregate-values) helped form a plan I'm happy with.

I imagine I will be displaying the values more than updating them--a user will see all of their `things` when they log in, but they may only want to update one during any given login session. So therefore it makes sense to store the current per-use value within the `userThing` model. Then whenever updates are made, I'll recalculate the value and post it as an update to the currentValue field.

In hindsight this seems pretty obvious.