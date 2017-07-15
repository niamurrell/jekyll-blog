---
layout:     post
title:      Postgres Success & Mongoose Intro
author:     Nia
tags: 		  Databases PostgreSQL Mongoose MongoDB
subtitle:  	Daily Review
category:   daily
---

### PostgreSQL Setup Success

Two days in a row! I got my Postgres server running after several hours troubleshooting. [This tutorial](https://www.codementor.io/devops/tutorial/getting-started-postgresql-server-mac-osx) proved to be the winner despite things not matching up entirely on my system. I had already installed both Postgres and pgAdmin 4 but couldn't run commands in the former and therefore had no idea where to start in the latter.

The issue turned out to be that whatever users are meant to be created in the "standard" installation process weren't created during my install. So following all of the other tutorials didn't work because I couldn't originally figure out how to see which users *were* in place. Once I figured out how to view, add, and edit users, and set their roles, I was able to get my setup to match the "standard" and next thing you know, **postgres success!!!**:

![connection!](https://s3.amazonaws.com/codementor_content/2016-Oct/postgres1/pg-admin-connected.png)

### Mongoose

 Got an intro to Mongoose in my bootcamp. [Mongoose](https://www.npmjs.com/package/mongoose) is an ORM (object relational mapping library) that turns JavaScript into MongoDB's query language. Similar to [Sequelize](https://www.npmjs.com/package/sequelize), which is what we'll be using in the group project with Postgres. Here is the basic setup for using it in an app and setting up a schema:

 ```
 // require Mongoose to be able to interact with db via JS
var mongoose = require("mongoose");

// connect to mongodb server. 27017 is default, can be checked in mongod terminal session
mongoose.connect("mongodb://localhost:27017/cat_app");

// create an inital model for the documents in the db
var catSchema = new mongoose.Schema({
  name: String, //data types must be capitalized
  age: Number,
  temperament: String
});

// compile the model into a variable which will be used to manipulate the db
// "Cat" must be singular version of your model name. Mongoose will create a collection of plural "cats" automatically based on your naming
// Compiling connects the new variable to a library of methods (Cat.find(), Cat.remove() etc.)
var Cat = mongoose.model("Cat", catSchema);

// create a new document as a new JS variable
var tiger = new Cat({
  name: "Tiger",
  age: 6,
  temperament: "shy"
});

// save the new document to the db and include error logs
tiger.save(function(err, cat) {
  if(err){
    console.log("something went wrong");
  } else {
    console.log("cat saved to database");
    console.log(cat);
  }
});


// alternate way to create and save a new document at one time
// must keep model and compile model in the file
Cat.create({
  name: "Skitz",
  age: 2,
  temperament: "crazy"
}, function(err, cat) {
  if(err) {
    console.log(err);
  } else {
    console.log(cat);
  }
});

// retrieve all cats from the database and console.log() each one with empty object + callback function
Cat.find({}, function(err, cats) {
  if(err) {
    console.log("an error occurred");
    console.log(err);
  } else {
    console.log("all the cats:");
    console.log(cats);
  }
});

 ```

### Other Stuff

Started reading [Think Like A Programmer by V. Anton Spraul](https://www.goodreads.com/book/show/18469872-think-like-a-programmer). Actually it was a free ebook library rental which I didn't know I could do! Rented from the library and downloaded from Amazon's Kindle store. Awesome. I'll let you know how it is.

### Up Next

Continuing work on the group project and bootcamp.

I'm also attending the [AT&T Shape Conference](https://shape.att.com/) tomorrow which is all about technology and entertainment converging...should be good!
