---
layout:     post
title:      Value App MVP COMPLETE!!!
author:     Nia
tags: 		  ValueApp
subtitle:  	Daily Review
category:   daily
---

***IT'S FINISHED!!!*** Tonight I finished the final missing piece for my [value app](https://niamurrell.github.io/search/index.html#ValueApp). Well...the last piece on v1.0 at least. It was all thanks to some help I got at a Meetup tonight...super stoked!


### New Approach To Deleting Dates

I had been really stuck on figuring out how to delete a single date from an array of dates. The array is a property in the MongoDB document, and the list of dates is populated to the site with a `forEach` loop.

My initial approach was a bit convoluted (in hindsight!):
1. Give each date an ID of that date
2. On click, event listener creates a variable of that date
3. Router takes that variable and looks for a match in the array with a `for loop`.
4. On finding a match, that date is deleted:

```javascript
var deletedUse = new Date(req.body.hiddenDateInput);
for (var i = 0, j = foundThing.usageDates.length; i < j; i++) {
	console.log(foundThing.usageDates[i]);
	if (foundThing.usageDates[i] == deletedUse) {
		foundThing.usageDates.splice(i, 1);
		break;
	}
}
foundThing.save();
```

This issue with this was that the date stored in the database was being captured by default in UTC time, while the newly created variable to search against was not. So going through the array, there would never be a match and no dates were being deleted.

Instead of this, the hero of the day recommended deleting the selected index of the array...that way you wouldn't have to worry about matching at all. I didn't know that the forEach function could take additional arguments...turns out [it can](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) and one of them is index! This was so much more straightforward:
```javascript
var index = req.body.usageDatesIndex;
foundThing.usageDates.splice(index, 1);
foundThing.save();
``` 

So now the app is fully functional and ready to deploy. Speaking of which...

### Yesterday's Issues

I really cracked myself up with that one [yesterday](https://niamurrell.github.io/daily/2017/12/11/grrrrrr/)! 😂😂😂 I figured out what I'd done wrong though—I was updating the dependencies to get ready to deploy, and used `npm update` out of habit, but I'd built the project using yarn. So after I'd "updated" some of the dependencies disappeared all together and the app crashed. Once I figured it out I ran `yarn upgrade` to get everything back to normal and it was all good!

### Ready to Deploy

I also got started on the AWS deployment. I'm trying Elastic Beanstalk but there's a bit of extra configuring to do in order to implement GitHub integration. I'm documenting the process step-by-step so will be good to have for future use.


### Up Next

Deploy deploy deploy!