---
layout:     post
title:      
author:     Nia
tags: 		  Algorithms CS50
subtitle:  	Daily Review
category:   daily
---

It's always the smallest things that can make your code not work!!

### Binary Search Algorithm

Today for me is was using less than `<` instead of less than or equals `<=`...as a result my binary search algorithm could only find its key in the top half of a sorted array, and returned `false` if the sought value was in the bottom half. I'm glad I figured out that it was working in any way--the original test failed--as this made it easier to narrow down what the problem was. In the end I got the function to search both halves correctly:
```javascript
// If value is in an array return true, else return false
// where value is an integer and values is an array of integers
function binarySearch(value, values) {
	while (values.length > 0) { 
		int l = 0, // Set left, right indices
				r = values.length - 1;
		while (l <= r) { // Terminate if left & right cross over each other
			int m = (l + r) / 2; // Set middle index
			if (value == values[m]) {
				return true;
			} else if (value > values[m]) {
					l = m + 1;
			} else if (value < values[m]) {
					r = m - 1;
			}
		}
		return false;
	}
	return false;
}
```

### Game of Fifteen

Next was writing a [Game of 15](https://en.wikipedia.org/wiki/15_puzzle) puzzle in C which can be played from the console. I hit so many brick walls I literally cannot write about or even think about this anymore! But I got it done : D

When I finally finished I was so excited I thought, "oh now I'll write it in JavaScript!" On second thought...

### Other Stuff

I came across a video of [Mark Zuckerberg doing a Q&A at CS50 in 2005](https://www.youtube.com/watch?v=xFFs9UgOAlE). It was interesting to hear him talk about what it was like building the first iterations of (The) Facebook--the data structures, size limitations, social concerns, etc. It's long (one to watch on double time) but interesting!

### Up Next

The next lecture & homework set is all about working with memory, recovering data, etc. I know very little about this so interested to understand more.