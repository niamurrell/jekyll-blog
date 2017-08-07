---
layout:     post
title:      Boot Camp Wrapup
author:     Nia
tags: 		  Libraries
subtitle:  	Daily Review
category:   daily
---

Officially finished with the online bootcamp...that's 43 hours of videos + all the time working! Lots of work went into it and I really enjoyed it and learned a lot. Including today, when I went back to the frontend part of the class to do the two projects I skipped during [Coding For Product](https://niamurrell.github.io/search/index.html#CodingForProduct). It was just building a simple JS to do app (no data persistence) and then a really cool [Patatap](http://patatap.com/) clone using a couple of libraries: [Paper JS](http://paperjs.org/) for the animations and [Howler JS](https://howlerjs.com/) for the sounds. 

Since the Patatap clone was a whole new concept and built on a library, it was a lot of reading the docs and copy/pasting, or just following along with the videos. The Paper JS library is really cool though, I'd like to get more practice building things with it from scratch.

The To Do app was mostly review of jQuery so I was able to write that on my own before watching the code along, for the most part. I did learn one clarification about using the `on` event handler which I wasn't aware of before...

### jQuery Event Handler `on`

I was aware of the difference between using `$(selector).click()` and `$(selector).on("click")`: the former listens for clicks on existing page elements only while the latter can also listen for events on elements created after the page has loaded (i.e. created as a result of something the user has done). What I didn't realize before is that `.on("click)` still needs its selector to be an existing page element in order to work; then the hypothetical elements can be added in as an argument of `on`. Here's an example of how you would listen for events on list items created by the user:
```javascript
$("ul").on("click", "li", function() {
	$(this).toggleClass("markDone");
});
```

What **won't** work is selecting the `li`s:
```javascript
$("li").on("click", function() {
	$(this).toggleClass("markDone");
});
```
This will work for any `li`s that are on the page when it loads, but nothing will happen to any new list items created by the user. Good to know!

### Up Next

It's weird being done with all of the big projects I was working on! Next to tackle at [CS50](https://www.edx.org/course/introduction-computer-science-harvardx-cs50x) and my portfolio page.