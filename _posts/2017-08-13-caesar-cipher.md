---
layout:     post
title:      Caesar + Vigenère Ciphers & Sorting Intro
author:     Nia
tags: 		  CS50 C
subtitle:  	Daily Review
category:   daily
---

### Caesar Cipher

Over the past couple of days I have been working on coding the [Caesar cipher](https://en.wikipedia.org/wiki/Caesar_cipher) in C for [CS50](https://niamurrell.github.io/search/index.html#CS50). While it seems pretty straightforward in theory, actually coding it was more complicated than I anticipated. The program takes any integer provided by the user as the key, and shifts the letters in the alphabet by that number to provide a coded message:
```
~/ $ ./caesar 45
plaintext: Hello, world! My name is Nia Murrell :)
ciphertext: Axeeh, phkew! Fr gtfx bl Gbt Fnkkxee :)
```

It sounded relatively easy at first since letters hold a numerical value (see [ASCII values](http://www.asciitable.com/)), so it should be as simple as adding the key value to the ASCII value and there's the code, right? Wrong. I won't post the code here (academic integrity policy) but basically, it was necessary to first convert the letter to its alphabetical index (`a=0`, `b=1`, etc.) and then shift by the key value, using the modulo `%` operator to make sure to keep looping through the alphabet (`XYZABC` rather than `XYZ[\]`). The assignment gave us the formula for the Caesar cipher (`cipherLetter = (plainLetter + userKey) % 26`) but without that alphabetic index conversion. Tricksy!


### Vigenère Cipher

The last problem for this week's assignments was to code the [Vigenère cipher](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher) which is slightly more complex than the Caesar cipher. Instead of shifting each letter by the same numerical key, there is a keyword and you shift each letter by the corresponding rotating key value. So the for loop required two variables--one for the key and one for the plaintext. Thankfully this one didn't take so long after understanding the basics from the Caesar cipher.
```
~/ $ ./vigenere candyfloss
plaintext: Hello, world! My name is Nia Murrell :)
ciphertext: Jeyom, kgjnd! Kd bseg vv Sto Ewrehjq :)
```

### Sorting Intro

In the next lecture we learned about different ways to sort data. 

**Bubble Sort**: 
```
repeat until no swaps
	for i from 0 to n-2
		if i'th and i+1'th elements are out of order
			swap them
``` 

**Selection Sort**:
```
for i from 0 to n-1
	find smallest element between i'th and n-1'th
	swap smallest with i'th element
```

**Insertion Sort**:
```
for i from 1 to n-1
	call 0'th through n-1'th elements the "sorted side"
	remove i'th element
	insert it into sorted side in order
```

All three of these methods run on the order of *n*-squared, so not very fast. This [comparison animation](https://www.cs.usfca.edu/~galles/visualization/ComparisonSort.html) shows how they each work.

**Merge Sort**:
```
on input of n elements
	if n < 2
		return
	else 
		sort left half of elements
		sort right half of elements
		merge sorted halves
```
Merge sort runs on the order of *n log n* so is faster than the other methods above. 

### Up Next

I took a quick glance at this week's homework assignments and surprise! Will be sorting lots of numbers.