---
layout:     post
title:      Workshop Day & Major App Work To Do
author:     Nia
tags: 		  Databases PostgreSQL CodingForProduct UI Testing Sass 
subtitle:  	Daily Review
category:   daily
---

Quick recap today as lots of new information has come in, and there's lots of work yet to do!

### Workshop Day

Yesterday was workshop day for **[Coding For Product](http://codingforproduct.com/)** so we had several talks:

#### Intro to UI/UX

Got some good detail about how much more there is to UI/UX than just the appearance of things. It has a much broader scope with a thorough process:
* Declare assumptions about your users to give the team a common starting point.
* Create problem statements to work on solving ((This user) needs a way to (do this thing) because (why they need to do it).).
* Create hypothesis statements to test your assumptions.
* Develop personas to better understand your target user.
* Analyze competition to see what other companies are doing to solve the problem, and think about how you can improve or innovate to differentiate your product.
* Conduct qualitative & quantitative research to test your hypotheses.

Then we talked about some ways to actually go about creating a product with all of this in mind (from sketches and wireframes to fully coded prototypes). And finally we went through the many different job roles that all fall under "UX/UI." Lots of interesting stuff!

#### Presenting A Product

We got another presentation about preparing for and presenting our product. In (now, less than) 2 weeks we not only need to have finished out app (!!) but we will also be presenting it to the workshop so lots to work on.

#### Intro To Sass

This was really great to see because I'd heard of sass (and less) before but didn't really know how to use them or how to even get started. We got a demo and saw that it's basically a separate file that you write with all of your styling, only you can nest elements so that there's a lot less writing to do in the actual css file. Then the `.scss` file is compiled (translated) into a normal `.css` file saving you a lot of time!

Sass requires Ruby to be compiled...that's where Less comes in if you'd rather not use Ruby just for this one function. Less is a node package that (with a few syntactic differences) pretty much does the same thing. I'm definitely looking forward to trying these out in the future!

#### Testing

We also got a very interesting talk on code testing, and how you can become a better programmer by testing your code throughout the process. This is something I have been really curious about--how can you write tests for code if you can't even figure out how to write the code that needs to be written!? Well turns out there are test runners with methods for each language which can be employed to help you write tests. While we didn't get many details on this aspect, it's defintiely something I will look into further--seems like a skill that's really necessary in the real world.

We also got a broader look at the Agile testing quadrants to see how testing and its many different facets come into play in a production environment:
![Agile Testing Quadrants](http://lisacrispin.com/wp-content/uploads/2011/11/Agile-Testing-Quadrants.png)

### Group Project

The countdown is on--no more workshops until the day we present and there is still quite a bit of work to do on our app:
* Configure PostgresQL database for our app (pretty much done)
* Add signup/login feature using [Passport](http://passportjs.org/) and [bcrypt](https://www.npmjs.com/package/bcrypt)
* Write JS function allowing users to choose a reward and then have their points balance deducted & updated in the database
* Deploy (!!!!) to Heroku
* Put together a quality presentation to demo the app

So I'm working on adding Passport and bcrypt at the minute and let's just say there is a lot to figure out. 😅

### Other Stuff

I will go more in depth about working with Postgres (now that I have it working!!) in a future post but definitely want to shout out this [PostgreSQL Command Line Cheat Sheet](http://blog.jasonmeridth.com/posts/postgresql-command-line-cheat-sheet/) which was a huge help in understanding what I was doing.

### Up Next

If I can get our login and encryption working in the next 48 hours I will be so happy. 🤓🤓
