---
layout:     post
title:     CSS Grid Intro & AWS Config
author:     Nia
tags: 		  CSS AWS
subtitle:  	Daily Review
category:   daily
---

Back home now after a few days out of town. Unfortunately I didn't have time to work on any of the projects or courses while I was away. But now back to studying. I'm finding getting motivation to work on CS50 a little bit difficult--still working on it but it's way less fun than other things I'd been doing in the past. Picking up a second thing to work on to have something to switch back and forth with really seemed to help a lot with [Coding for Product](https://niamurrell.github.io/search/#CodingForProduct) so I am going to start doing that.

### Portfolio Site & CSS Grid

Since it's been in the 'up next' pile for a while, I jumped back into creating my dev portfolio website. Rather than relying on Bootstrap I'm going to learn CSS Grid for this site, and spent some time today getting introduced via a few YouTube videos:

* [How to create website layouts using CSS grid by mmtuts](https://www.youtube.com/watch?v=HgwCeNVPlo0) is a basic demo showing how things move around, and some basic properties like spacing and alignment.
* [CSS Grid Layout Crash Course by Traversy Media](https://www.youtube.com/watch?v=jV8B24rSN5o) is another basic demo similar to the above, moving around generic divs to see how the grid works.
* [Build a Mosaic Portolio Layout with CSS Grid by Kevin Powell](https://www.youtube.com/watch?v=plRcoRqLriw) shows an interesting way to lay out a portfolio (what I need to do!) but again, stays fairly demo. Interestingly, he puts a grid inside of a flexbox layout...isn't grid meant to take the need for flexbox away?
* [Creating a nice layout CSS Grid layout using grid template areas by Kevin Powell](https://www.youtube.com/watch?v=v5KzBPUEgGQ) is a much more practical demo, showing how to lay out a whole web page using grid, including how to make it somewhat responsive.

After watching these demos I thought it may be helpful to just read the documentation to try and get a bit more familiar and came across a few helpful sites:

* [Learn CSS Grid](http://learncssgrid.com/)
* [Grid By Example](https://gridbyexample.com/) which shows a lot of examples of different layouts you can do with CSS grid. Written by Rachel Andrew who apparently is *the* CSS Grid evangelist & contributor. She gave a [great talk](https://www.youtube.com/watch?v=tjHOLtouElA) I watched a few weeks back.
* [MDN docs](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout) haven't dived into this yet but no doubt a key source

While this is a lot to take in and I'm still not 100% sure where to start, it's worth mentioning the video I watched a few weeks back which peaked my interest in the first place: [CSS Grid Changes EVERYTHING](https://youtu.be/7kVeCqQCxlk), a talk by Morten Rand-Hendriksen from WordCamp Europe 2017.

Looking forward to learning this!


### AWS Setup

Another big thing on the to-do list was finally setting up a working subdomain on my website, where I plan to host my portfolio once I build it: [dev.niamurrell.com](https://dev.niamurrell.com). I have been learning Amazon Web Services for hosting [my personal site](https://niamurrell.com) but I'm realizing that every time I want to implement something new, there is a ***steep*** learning curve to get even the simplest-seeming things working.

Case in point: about 2 months ago I figured out how to add an SSL certificate so that my site is on `https` rather than `http`. Since AWS offers free certificates for their hosted domains it should be simple, right? Not exactly. The certificates can only be linked with certain services, not including S3 web hosting for static sites which was how my site was working up until then. So I had to create a CloudFront distribution, point the S3 bucket to that, and then set up a DNS nameserver alias linking to CloudFront for the SSL certificate to work. That took quite a bit of time and configuring to make it work, but it got there in the end.

Next I created dev.niamurrell.com as a subdomain of my main site and copied all the settings, so it should have worked in the same way, right? Nope! I kept getting an error page which had no helpful information on it, and then [Coding For Product](https://niamurrell.github.io/search/#CodingForProduct) and the [online bootcamp](https://niamurrell.github.io/daily/2017/08/06/bootcamp-wrapup/) took priority, so I just let it be.

Well today I picked it back up and it took a couple of hours to realize there was one simple setting that needed adjusting--of course! When you set up an S3 bucket for website hosting, it prompts you to elect a root file and an error file as defaults for when people visit the site, which I had done. Today I learned that you must also make the election (again) in CloudFront, even though this field is marked 'optional' in the settings. Otherwise it will just route to a server document instead of the desired content. More about this in the [AWS docs](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/DefaultRootObject.html).

So now I got it working and have a pretty good understanding of how the whole system works for static sites. Next up will be setting up an app with a server, which will probably come pretty soon in order to include the more advanced projects in my portfolio.


### Up Next

I want to keep the momentum up on CS50 even though it's getting harder! And keep working on my dev site.
