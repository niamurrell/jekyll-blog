---
layout:     post
title:      Value App Finished!
author:     Nia
tags: 		  ValueApp JavaScript
subtitle:  	Daily Review
category:   daily
---

Value App is finished! 

Well, functionally finished that is. All of the logic, date additions, etc. are all fully functional in the app. Super happy about that! I do still have quite a bit to work on though.

### JavaScript Date Object

This is a new beast whose tricks I'm slowly learning. First all my dates were coming in as strings which doesn't necessarily change the function of the app, but doesn't strike me as being good practice either. To fix this I added the Date object on top of the incoming form data: `purchaseDate: new Date(formDateInputField)`. 

Next I ran into browser issues with this whole setup. In Chrome, there is a calendar dropdown which seems helpful, except that the calendar records UTC time while my computer is several hours behind. This means that no matter what date I pick on the calendar, the day after is what's being saved to the database. Not ideal. In Firefox it saves it as my local timezone, but you have to manually type in the date each time. Also not ideal. 

Two fixes for this I will experiment with: first I want to add my own JS visual date picker which will populate the date input to make it easier to use. Second I'm going to try the MomentJS npm package which looks like it handles time zones and date displays better than the basic JS date object. Added bonus, I can style the site with relative time (like '2 days ago' etc.) which I think will look pretty cool.

### Styling The Site

Also to do: need to style the site and make it look nice. It looks like crap right now.

### Editing Things

The way you edit a `thing` right now isn't great, and I'd like you to be able to remove accidental `uses` too, so will need to massively re-do this page & route.

### And More Features

I also want the app to support subscription-type `things` like gym memberships or TV services where you pay monthly or quarterly. Right now the purchase price is set in time and the per-use price is calculated from that. I want to be able to track `things` accurately if you have to put more money into it. And currency support!

### Up Next

Going to fix the dates before styling so that I can start to use the app myself. Then styling. Also would like to finish this week's CS50 homework before the week's end.