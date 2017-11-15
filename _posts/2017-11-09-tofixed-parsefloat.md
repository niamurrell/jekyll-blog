---
layout:     post
title:      JavaScript Numbers - toFixed, parseFloat, toLocaleString
author:     Nia
tags: 		  JavaScript ValueApp
subtitle:  	Daily Review
category:   daily
---

More work on my [value app](https://niamurrell.github.io/search/index.html#ValueApp) today which I'm naming valueMax for the time being. I'm meant to be styling the site but there turned out to be some functional kinks to iron out.

### toFixed & parseFloat

While working on styling the site, I decided to change the main display from showing the date purchased to showing the current cost-per-use of each thing. I wanted to to look like currency, so tried to use `toFixed(2)` to guarantee two decimal places on each price. This threw a huge error `Cannot read property 'toFixed' of undefined` every time, but I couldn't figure out why. `toFixed` is a vanilla JavaScript method so why wouldn't it work in my code? Hmmm..

Some stackoverflowing gave a good clue that `toFixed` only works on numbers and will throw an error on strings. I know I'm saving the number as a number in my database, but could it be rendering to the page as a string? First I double-checked that it was indeed a number in the database using [Robo 3T](https://robomongo.org/), and confirmed all prices with cents are being stored as a `double`, so that should be fine.

I also thought about forcing the current value to always be stored in the database with two decimal places. But then quickly ruled that out...the more times the number is divided, the less accurate the output would be if I limit the number of decimal places. So no go.

Next thing to try to was make sure my `currentValue` is indeed a number before using `toFixed`, and this is where `parseFloat` comes in: `parseFloat(thing.currentValue).toFixed(2)`. This turns `thing.currentValue`, which is a number rendered as a string, back into a number, to then be fixed to two decimal places. 

And it worked! **So lesson learned: no matter how a number is stored in the database, it will be rendered as a string in the front end. To manipulate the number for display, it needs to be made a number again to avoid errors.** I think I had learned this before in a class but I guess it takes working on it properly for it to stick.


### toLocaleString

Happy with this result my next aim was to display separators in the prices, so `11324893.67` would display as `11,324,893.67`. And this led me to `toLocaleString` ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString))! This is a method that will add separators based on the locale of the user's OS. So for example US currency will display `$11,324,893.67` while those in Italy for example will see `€11.324.893,67`. So this actually killed 2 birds with one stone--sweet!

I'm not 100% sure I'll keep this as my method of currency support--what if a user makes purchases in different currencies for example? As someone with obligations in the US and the UK, I find it pretty annoying when sites allow my browser to determine what content & functions I have access to. But anyway good to know `toLocaleString` exists!--I'll keep it for now and improve later.


### Up Next

Style the single `thing` view. Then do another pass on all the styling.