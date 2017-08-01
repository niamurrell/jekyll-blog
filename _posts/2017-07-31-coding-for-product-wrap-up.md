---
layout:     post
title:      Coding For Product - That's A Wrap!
author:     Nia
tags: 			CodingForProduct JavaScript AJAX Deployment
subtitle:  	Daily Review
category:   daily
---

And that's a wrap! Yesterday we (quasi-) finished and (actually) presented our Rides For Rewards app ([demo](https://rides-for-rewards.herokuapp.com/) / [code](https://github.com/CodingForProduct/metro_reward) / [presentation](https://youtu.be/6hn4tIg2IT4?t=1h1m5s)) for [Coding For Product](http://codingforproduct.com/). In the end I'd say we got 92% of the way to where we set out to go in the beginning when we came up with the idea, and for never having built an app from scratch before, and completing the project in 5 weeks, I think that's pretty good!

We spent most of Saturday trying to get the project over the line. The main tasks were getting our points deduction function to work, and deploying. Both turned out to be more difficult than I think any of us expected.

### JavaScript & AJAX

The big lesson here was that client-side JavaScript and server-side JS can't communicate with each other by default. This was news to us as I had been trying to validate usernames in the database as unique from the front end, and one of my teammates was trying to update the user's points balance from the front end...both of which we learned is not so simple! In the end, because we were using jQuery in some of the front-end code, we figured out at the last minute how to use AJAX to send this information to the server in our front end code:
```javascript
modalConfirm(function(confirm) {
	if(confirm){
		totalPoints = getBalance(totalPoints, redeemPoints);
		$.ajax({
			url: '/myrewards',
			method: 'POST',
			contentType: 'application/json',
			data: JSON.stringify({ points: totalPoints }),
			success: function(){
				window.location = "/home";
			}
		})
	} else {}
})
```

Then in the `app.js` file we added a route to accept the information and update the user's details in the database, and then send a success message back to the front end for AJAX to redirect to a new page which would show the points deduction went through successfully:
```javascript
app.post("/myrewards", isLoggedIn, function(req, res) {
  var pointsTotal = req.body.points;
  User.update(
    { pointsBalance: pointsTotal },
    { where: { username: req.user.username }})
	.then(() => {
			res.json({status: "Success", redirect: "/home"});
	})
	.catch(err => {
			console.error(err);
	});
});
```

While this may not have been the most efficient way to make this work, it was good to get a crash course on AJAX and to know what's possible/necessary if it comes up again. I think next time this would ideally be posted to the server to process the points redemption and then redirect to a new page...or better yet have the whole thing be a single page app that's all rendered client-side and avoid page refreshing all together. So, more to learn about later!

### Deployment

This was also the first time anyone on my team deployed an app with a database attached and the environment file and variables we were using in development brought up unknown issues once we tried to get things working in a production environment. Although it turned out to be a simple solution (add an `if` statement around the `dotenv` package to make sure it's ignored in production, and identify the correct .env variables for Heroku), being the first time it took a while to figure out. Glad to know what to do next time though.

### Workshop Wrap-Up

In the end I am so happy I took part in [Coding For Product](http://codingforproduct.com/), and I'm still amazed that a program like this exists for free to the participants, and all built around volunteered time from the lead instructor & organizer Wai-Yin Kwan and the program mentors. Since I never really explained what it is in [earlier posts](https://niamurrell.github.io/search/#CodingForProduct) it's worth a quick recap:

* 20ish students put into small groups on day 1 to come up with an idea for a web app and build it from scratch in 5 weeks. We were all skill levels from beginner to employed developers, and apps were built in JavaScript, Python, and Ruby.
* Weekly workshops where we heard presentations from a great host of people from many different tech backgrounds about a wide variety of topics applicable to working as a developer including:
    * Product Design & UX (user stories, empathy maps, wireframing, etc.)
		* Intro to different kinds of web apps
		* Project management tools & collaboration workflows
		* Design frameworks like Bootstrap & Foundation, Sass
		* Intro to working with databases, SQL, and data modeling
		* Authentication & Authorization
		* Deployment
		* Presenting A Product & Communicating with Non-Devs
    * Professional development & discussion about entering the workplace
* 12+ hours/week to actually build our app, have group meetings, study, etc.
* Community support from companies like [GitHub](https://github.com/), [O'Reilly](https://www.oreilly.com/), [Rosenfeld Media](http://rosenfeldmedia.com/), and [Frontend Masters](https://frontendmasters.com/) who donated learning resources and discounts and the like to everyone who completed the workshop
* And all hosted at the lovely offices of [Philosophie](https://philosophie.is/), where they shared not only the physical space but also the expertise we gained from several of the workshops listed above. Plus they had free parking, great wifi, and snacks! 💃🏽 💃🏽 

Written out like this it's pretty cool to see just how much information we got and how much work went into this from so many people! It was a lot of work on our end too, and well worth it--I don't think it's a stretch at all to say I learned more in these 5 weeks than I had in the 5 months prior learning on my own. So on the off chance any of the volunteers, mentors, presenters, hosts, or swag donors ever read this, a huge and eternal thanks for supporting the workshop and making all of this possible!!

### Up Next

We've decided to keep working on our app as a group to finish out some of the functionality that we didn't quite get to in time, and to make improvements as we get more skills. I really enjoyed working with my teammates so glad we'll keep in touch and keep working together in some form or another. Some other workshoppers also mentioned the possibility of collaborating on new projects to keep building expertise which I think would be great! 

More immediately I'll be getting back into the computer science class I put on hold when CFP started. And of course some last things to wrap up with the online bootcamp. So on we go!