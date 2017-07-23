---
layout:     post
title:      Slowly Making Progress
author:     Nia
tags: 		  CodingForProduct Authentication Alexa
subtitle:  	Daily Review
category:   daily
---

Today our group met to attack this login/authentication problem and we made some progress!! It really helps to talk through a problem with other people. The whole login/authentication thing is just as new to my teammates as it is to me so we're all kind of in the dark, but even so putting three heads together got us farther along than I probably would have gotten carrying on as I had been.

### Login Progress

So the main development was that we have been able to query our Postgres database (via sequelize) to compare the 'username' entered by the user on the login page with existing users.

I should back up--the progress over the past week, once my teammate got our app connected with the database (a **huge** feat, seriously!), was configuring the 'signup' form to successfully post the new user's account details to the database. Also included in that was hashing the password for security, and putting validation against the form (unique email address, password with security criteria, etc.).

So now that users can successfully and securely sign up for the site, we need to allow them to log in and use the app from their own account. And this is where it got difficult. Configuring the `passport` module and all of its dependencies has proven to be incredibly tough. But today we at least got it to check for an existing user given the email address entered in the login form.

Next we tried to pull that user's hashed password from their record, convert it to plaintext, and compare it against the password they entered on the login form. For so many reasons, we couldn't get this working. So we reached out to some of the mentors in our project and were advised to check the password outside-in rather than inside-out...that is, hash the password they enter on the form and see if that hash matches the hash stored in the database. So that is the next step to try and get it working...fingers crossed!

### Alexa Skills Workshop

I also went to an Alexa Skills workshop hosted by the Coding Dojo bootcamp. Amazon is clearly in growth and outreach mode when it comes to Alexa, and I have to hand it to them for the way they've gone about things. Basically they need to crowdsource "skills" for Alexa (commands/programs that can happen when you interact with the [Alexa products](https://www.amazon.com/Amazon-Echo-And-Alexa-Devices/b?ie=UTF8&node=9818047011)), so they're recruiting companies like Coding Dojo to run developer workshops in the hopes that more people will code some skills and submit them to the Skills Library. They're actually taking it further than that--if you register as having attended an event and then submit 3 skills to their library, they automatically send you a free Alexa device! Considering they retail for $50+ and basic skills are pretty easy to code if you're comfortable with JavaScript and JSON objects, it's not a bad deal at all for someone who likes gadgets. I might give it a try when we finish our project...although I don't really want a device constantly listening in my home but I guess that's another story!

### Up Next

We're down to the wire on our group project now--presenting a week from tomorrow--so that will be the main focus. Not sure there will be much time for anything else!
