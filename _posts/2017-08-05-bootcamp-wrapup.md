---
layout:     post
title:      Heroku Workflow & Intro to Advanced Topics
author:     Nia
tags: 		  Heroku Deployment This OOP New Closures
subtitle:  	Daily Review
category:   daily
---

Today I quasi-finished the online bootcamp course. Quasi- because I still have to go back and do two sections I skipped, but I completed the big app project and the "advanced topics" section. Annnd to be honest 'completed' might be a bit strong too--while I got a LOT out of doing the bootcamp, it kind of seems like they never finished making the course? It just kind of stops midway through the project so I'll have a lot of refining to do on my own. Not that that's a bad thing!

### Heroku Deployment

I deployed the bootcamp project we've been working on to Heroku [link](http://firecamp2017.herokuapp.com/) which was pretty straightforward after doing the previous apps. Good to know I'm comfortable with that! For future reference here is the typical order of commands:

1. Add to package.JSON:
```
"scripts": {
	"start": "node app.js"
}
```
2. `heroku login`
3. `git init` then add & commit all if not already a git repo
4. `heroku create`
5. `git push heroku master` + during this process production environment variables are created:
```
NPM_CONFIG_PRODUCTION="true"
NODE_ENV="production"
```
6. Check for errors to debug 'Application Error' with `heroku logs`
7. Rename the app with `heroku apps:rename newName`
8. Destroy an app with `heroku apps:destroy -a app-name-12345 --confirm`
9. Set environment variables with `heroku config:set KEY=VALUE`
10. Use the heroku CLI with `heroku run`... (ls, cd, mkdir, etc.)

### The Keyword This

One of the advanced topics in the last section of the course was about using the keyword `this` in JavaScript. Some things to remember:

1. The value of `this` is determined by the execution context, i.e. how the function was called.
2. When `this` is used outside of a declared object, it refers to the **window**, i.e. has a global context.
3. When `this` is inside a declared object, it refers to the ***closest* parent object**. It's important to remember *closest* when dealing with nested functions.
4. You can set the value of `this` using `call`, `apply`, or `bind`.

### Object Oriented Programming

We also covered the basics of OOP, and how to use classes as blueprints to create new objects. Coincidentally the keyword `new` comes up a lot! Som basics...

**Constructor functions** are abstract and modular so that they can be shared and reused within an application. By convention, a constructor function will be Capitalized. The keyword `new` is used to create a new object from the constructor; it automatically does four things:
1. Creates an empty object
2. Attaches the keyword `this`
3. Implies `return this` has been added at the end of the object
4. Adds the "dunder proto" (`__proto__`) property which links the new object to the constructor function's `prototype` property

**Multiple constructor functions** can be nested with `call` and `apply` to make code more DRY:
```javascript
function Car(make, model, year) {
	this.make = make;
	this.model = model;
	this.year = year;
	this.numWheels = 4;
}

function Motorcycle(make, model, year) {
	this.make = make;
	this.model = model;
	this.year = year;
	this.numWheels = 2;
}
```

The motorcycle function can be refactored in multiple ways:
```javascript
function Motorcycle(make, model, year) {
	Car.call(this, make, model year);
	this.numWheels = 2;
}
```

```javascript
function Motorcycle(make, model, year) {
	Car.apply(this, [make, model, year]);
	this.numWheels = 2;
}
```

```javascript
function Motorcycle(make, model, year) {
	Car.apply(this, arguments);
	this.numWheels = 2;
}
```

**Prototypes** help make code even DRYer still since `__proto__` is accessible by all objects made from the constructor. Rather than calling a function inside of a constructor, it's better to call it using a prototype, so that the function doesn't have to be repeatedly defined:

```javascript
function Person(name) {
	this.name = name;
	this.sayHi = function () {
		return "Hi " + this.name;
	}
}

nia = new Person("Nia");
nia.sayHi() // Hi Nia
```

Instead it's better to write:
```javascript
function Person(name) {
	this.name = name;
}

Person.prototype.sayHi = function() {
	return "Hi " + this.name;
}

nia = new Person("Nia");
nia.sayHi() // Hi Nia
```

### Closures

Finally, we were introduced to closures: functions that make use of previously returned variables defined from outer functions:
```javascript
function outer() {
	var data = "closures are ";
	return function inner() {
		var innerData = "awesome"
		return data + innerData
	}
}

outer() //function inner() {
		// var innerData = "awesome"
		// return data + innerData
	// }

outer()() // "closures are awesome"
```

From the little I've learned about ES6 it seems to me that the new `let` and `const` variables might accomplish the same thing as closures? I need to look into that more.

### Other Stuff
I came across [this developer roadmap](https://github.com/kamranahmedse/developer-roadmap) again today...the first time I saw it was maybe a month or two ago. It was nice to recognize that in that short time, I already know more things on this map than I did the last time I looked at it!

### Up Next

I don't know how realistic it is to finish up the bootcamp completely this weekend but I really want to. I also want to get my personal portfolio up and running so I have somewhere to put all this stuff. Maybe I will prioritize the portfolio--it's a lot easier to do tutorials after work than build something from scratch!