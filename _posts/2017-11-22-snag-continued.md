---
layout:     post
title:      Snag Continued
author:     Nia
tags: 		  ValueApp JavaScript Node Express MongoDB
subtitle:  	Daily Review
category:   daily
---

I am still working on trying to fix the [bug](https://niamurrell.github.io/daily/2017/11/20/snag/) I came across recently and have done a few back-and-forths about how to address it.

### #1: AJAX Research

When I left off before I thought updating the value using an AJAX request may be a good fix. On second thought, it's not. There is already a page reload in place for editing the `things`, so I should be able to carry out the operation on the server as the data are being updated through this page's PUT route. 

An AJAX request would be a great solution if I weren't already serving the page through Express routes...in fact maybe in a future refactor this could be a more seamless way to do all of the page updates. But in this case, it didn't seem right or necessary to scrap all of the page routing because of this one hurdle.

### #2: Create Object From Form Data

Back to the original plan to submit updated information from the form and use this with the `findByIdAndUpdate` Mongoose query method. The issue before was that the `useCount` and `currentValue` were not part of the form, and one or both of these would be required to include with the update. So I got to finding a way to include them, with two options:

1. Calculate the new `currentValue` on the fly, or 
2. Add the `useCount` to the form.

Option 2 doesn't make much sense from a UI perspective, so I went for option 1. To do this I attached an event listener to the input field where the user can update the original purchase price. As they edit the number there, a second, disabled field is updated to show what the new cost-per-use will be.

On second thought, because this display number will be rounded to two decimals, if I use this field to update the value in the database, eventually the numbers could be off due to rounding. Not good!

So back to plan A of including the `useCount` on the form somehow. And that's where I'm stuck at the moment.

### Creating An Object From Form Data

Now I have all the possible fields on this form, matching the fields in the database model being updated. But for some reason (which I'll be figuring out tomorrow hopefully) only half of the object is being created from the fields in my form. Each input field has an attribute which should create an object: `thing[name]`, `thing[purchasePrice]`, `thing[purchaseDate]`, `thing[useCount]`, etc. This should create and object:
```javascript
var thing = {
	name: "input value",
	purchasePrice: inputValueNumber,
	purchaseDate: inputDate,
	useCount: numberFromExistingVariable
}
```

Only the first two are showing up in the object. So up next is to figure out how to get the others added as well, so that all of the necessary info can be updated with the PUT route.

### Up Next
↑