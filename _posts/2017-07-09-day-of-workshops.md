---
layout:     post
title:      Authentication & Deployment & Data Models & More!
author:     Nia
tags: 		  Deployment Databases CodingForProduct Node Express Tools
subtitle:  	Daily Review
category:   daily
---

Workshop day for Coding For Product so picked up ***lots*** of new information in today's talks:

### APIs, Authentication, & Authorization
Learned that browsers have a single origin policy meaning it will only process information from items on the same or a similar domain. This makes things tricky when working with APIs from different sources, and explains why you need a server to process them. It also can explain why you need to host your own fonts (except for Google fonts somehow?). Also picked up some new terms to be aware of on this topic: JWT (JSON web tokens), CORS (cross origin resource sharing...helps resolve single origin issues), and curl, a way to imitate a browser from the command line.

### Deployment
We're getting close to when we'll need to make our app public(ish) so was helpful to get more info about deployment options. Definitely handy to get a list of cloud server options: Rackspace, AWS, Microsoft Azure, Openstack, Google Cloud Platform, and Digital Ocean to start. We also picked up some deployment best practices to keep in mind:
* TEST TEST TEST before deployment!!
* Always keep backups
* Know how to roll back to a backup *before* deployment
* Keep an audit trail of deployments as well as log statements in the code to make it easier to track down when/where things break
* Always test after deployment! 'Deployment' isn't finished until you've deployed ***and tested***!


### Data Modeling
This was a key piece of information I didn't really have a grasp on before, and it was really helpful to learn as we're in the process of modeling and creating our database structure for the app we're building.

An **ERD** (entities relational diagram) is a standardized illustration of how the tables in a database will relate to each other and it's drawn with specific symbols and meaning. *Entities* ("tables," "collections," etc.) have different relationships to each other, described by *cardinality*: one-to-one, one-to-many, or many-to-many (which requires a join table). [Here](https://stackoverflow.com/questions/20850160/which-erd-is-more-correct-re-proper-database-design) is an example of an ERD in the context of a debate on Stack Overflow. Also good to know: [LucidChart](https://www.lucidchart.com/) is a good tool for building these diagrams.

### Other Stuff
Also learned about some additional tools which will probably be helpful for building our app:
* `express-ejs-layouts` (npm package) lets you set a standardized layout for all the pages on your site, so that you don't have to repeat `include` statements in each page file.
* `.env` files are how you keep sensitive information out of public repositories and can still collaborate with other people on the project.
* `passport` is another npm package which handles user login with Node and Express.
* Got stuck on another layout issue which was solved again with a CSS `float`. Reminder to self: always try a float!!

### Up Next
This week I'm tasked with finishing up the UI on our app and setting up the user login feature. UI should be alright except that I'm so nitpicky about the aesthetics! Login is totally new so excited to learn how to do that.
