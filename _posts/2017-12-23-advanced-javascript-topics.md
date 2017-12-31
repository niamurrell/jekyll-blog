---
layout:     post
title:      Advanced JavaScript Topics
author:     Nia
tags: 		  JavaScript Closures Scope Underscore
subtitle:  	Daily Review
category:   daily
---

Today I finished the Frontend Masters course, and we dug deeper into some advanced JS topics. Some of it was recap and some of it was new:

### Scope

Where variables have their meaning. Some good reminders on the rules of scope:
* Scope is created dynamically when we run a function, i.e. when we open a new execution context.
* A function has access to its own local scope variables, and inputs to a function are treated as local scope variables. A function has access to variables in higher generation scopes (parent, grandparent, global, window, etc.), but not sibling of child scopes.
* A function's local scope variables are not available anywhere outside that function, regardless of the context it's called in:

```javascript
var ACTUAL = null;
var firstFn = function () {
	var localToFirstFn = 'first';
	secondFn();
};

var secondFn = function () {
	ACTUAL = localToFirstFn;
};

secondFn(); // error
firstFn(); // ACTUAL === null
```

* If an inner and an outer variable share the same name, and the name is referenced in the inner scope, the inner scope variable takes precedence. This makes the outer scope variables inaccessible from anywhere within the inner function block. If the name is referenced in the outer scope, the outer value binding will be used.
* A new variable scope is created for every call to a function:

```javascript
var fn = function () {
	var localVariable;
	if (localVariable === undefined) {
		ACTUAL = 'alpha';
	} else if (localVariable === 'initialized') {
		ACTUAL = 'omega';
	}
	localVariable = 'initialized';
};

fn(); // ACTUAL === 'alpha'
fn(); // ACTUAL === 'alpha'
```

* An inner function can access both its local scope variables and variables in its containing scope, provided the variables have different names
* Between calls to an inner function, that inner function retains access to a variable in an outer scope. Modifying those variables has a lasting effect between calls to the inner function:

```javascript
var outerCounter = 10;

var fn = function () {
	outerCounter = outerCounter + 1;
	ACTUAL = outerCounter;
};

fn(); // ACTUAL === 11
fn(); // ACTUAL === 12
```


### Module Pattern

Writing modular functions allows you to set private methods (`useGas`) and private properties (`gasLevel`) which can only be accessed by privileged functions (`go`) to prevent manipulation from the outside on variables that should have set limits:

```javascript
var Car = function() {
	var gasLevel = 10;
	function useGas(amt) {
		if (gasLevel - amt < 0) {
			console.log("Out of gas :(");
		} else {
			gasLevel -= amt;
		}
	}
	return {
		radioStation: "104.1",
		changeStation: function(station) {
			this.radioStation = station;
		},
		go: function(speed) {
			useGas(speed);
		}
	};
};
```


### Underscore.js Library & each(), map(), filter()

The [Underscore](http://underscorejs.org/) library adds a lot of methods to the underscore symbol: `var _ = {...}`. We did a lot of exercises with `_.each()`, `_.map()`, and `_.filter()`.

#### _.each()
`_.each()` iterates over a list of elements; the iterator comes with three parameters:

```javascript
_.each([1, 2, 3], function(element, index, wholeThing) {
	// do something
})
```

To invoke the `_.each()` method, the function takes two parameters: a **list** (array or object) and an **iterator function**. Note: the native JavaScript `forEach` method only works with arrays. With `.each()` you can ***not*** *return* any values in the loop. Example:

```javascript
var pokemon = ["Evie", "Growlithe", "Vulpix"];
var logger = function(val) {
	console.log(val);
}
_.each(pokemon, logger);
// Evie
// Growlithe
// Vulpix
```

#### _.map()
`_.map()` iterates over a list of elements and returns a new list of values by mapping each original value through a transformation function (iterator). With `_.map()` you ***must*** *return* a value in the iterator function so that there is a value to go into the array.

```javascript
var makeExcited = function(val) {
	return val + "!!!";
}

_.map(pokemon, makeExcited); // ["Evie!!!", "Growlithe!!!", "Vulpix!!!"]
```

Note that all of these functions work the same way, by running a function as though it has three arguments: `function(element, index, wholeThing)`. If the function doesn't have three arguments, it assumes the first, or first 2 if there are two present.

#### _.filter()
`_.filter()` iterates over a **list** and returns an array containing only the values that pass the **tester** function (aka predicate): `_.filter(list, tester)` Example:

```javascript
var evens = _.filter([1,2,3,4,5], function(num) {
	return num % 2 === 0;
});

console.log(evens); // [2,4]
```

#### Using Objects Instead of Arrays

These methods work on both arrays and objects. To access the keys & values of objects you can look at the parameters of the function as `function(value, key, object)` instead of `function(element, index, array)`. Example:

```javascript
var input = {
	two: 2, 
	four: 4, 
	three: 3, 
	twelve: 12 };

var myNums = _.map(input, function(val, key, obj) {
	return val;
})

console.log(myNums); // [2, 4, 3, 12]
```


### Up Next

Keep working on Hexo site. It's coming along nicely and definitely want to have it up by the 31st.