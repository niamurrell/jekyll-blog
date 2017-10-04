---
layout:     post
title:      Dates in JavaScript
author:     Nia
tags: 		  JavaScript ValueApp
subtitle:  	Daily Review
category:   daily
---

Doing a bit of reading up to try and get my dates working properly in the [value app](https://niamurrell.github.io/search/index.html#ValueApp). I found a great article on [UX design guidelines for date/time inputs](https://www.nngroup.com/articles/date-input/)...it has some pretty good examples on what I'm trying to avoid!

### Moment.js

I added [Moment.js](https://momentjs.com/) to give more control over how my dates are displaying in the app. By default they all displayed in UTC time (`Sun Aug 27 2017 17:00:00 GMT-0700 (PDT)`) but obviously this is ugly. Yesterday I got it to look a bit better by appending `toDateString()` to the date which was a bit better: `Sun Aug 27 2017`. With moment I can set the date to any format I want, for example `moment(thing.purchaseDate).format("dddd, D MMMM YYYY")` displays `Sunday, 27 August 2017`. Much better! And of course I can change the format any number of ways, and also eventually add support for users to select their own format.

### Datepickers

I also needed to solve the issues presented by using the `input type="date"` form field which acts very differently in different browsers (see [yesterday's post](https://niamurrell.github.io/daily/2017/10/02/value-app-finished/) for details). The rabbit hole led me to jQuery UI which has a [datepicker widget](http://api.jqueryui.com/datepicker/). Super helpful because I didn't even know jQuery has a UI API before this. This [jQuery UI Intro](https://www.youtube.com/watch?v=NoH41RObujo) on YouTube, as well as this [intro to the datepicker](https://www.youtube.com/watch?v=tkKrvgANv8A) helped me get set up pretty quickly.

And the best of all: using this means using `input type="text"` instead of `input type="date"` which I picked up from the [Chrome developer FAQs](https://developers.google.com/web/updates/2012/08/Quick-FAQs-on-input-type-date-in-Google-Chrome). By using the datepicker to input the date as text instead of a JavaScript date object, it now uniformly enters the date in the user's timezone in all the browsers I am able to test.

So all in, got all the date issues ironed out and now ready to move on to styling the site. But it works!

### Other Stuff

I finished Ariana Huffington's book [Thrive](https://www.goodreads.com/book/show/18594634-thrive) which introduces a ***third metric*** to measure success by (in addition to the metrics of money & power, which everyone already seems to be pretty comfortable judging others by 😁): one's ability to thrive. "Thriving" combines one's wellbeing, intuition, spirituality, and positive habits. It was a quick and encouraging read I'd recommend!

### Up Next

Keep working on the value app & deploy it in the next couple of weeks.