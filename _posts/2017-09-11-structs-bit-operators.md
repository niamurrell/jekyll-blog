---
layout:     post
title:      C Structs & Bit Operators
author:     Nia
tags: 		  C CS50
subtitle:  	Daily Review
category:   daily
---

### Structs In C

I keep having to go back and look this up so lets keep it here for reference:

```C
// Variable Declarations
struct *mycar = malloc(sizeof(struct car));

// Accessing Fields
mycar->year = 2006;
mycar->odometer = 7519
```


### Bit Operators in C

There was a bit of code that made no sense to me and took some digging to figure out. In the program I'm writing to recover .jpg files from an erased memory card, we are meant to find the beginning of each .jpg file by looking for a file signature: each .jpg file always starts with 4 specific bytes described below:

*Specifically, the first three bytes of JPEGs are `0xff 0xd8 0xff` from first byte to third byte, left to right. The fourth byte, meanwhile, is either `0xe0`, `0xe1`, `0xe2`, `0xe3`, `0xe4`, `0xe5`, `0xe6`, `0xe7`, `0xe8`, `0xe9`, `0xea`, `0xeb`, `0xec`, `0xed`, `0xee`, or `0xef`. Put another way, the fourth byte’s first four bits are `1110`.*

The code we were given to write this simply is:
```C
if (byte[0] == 0xff &&
	byte[1] == 0xd8 &&
	byte[2] == 0xff &&
	(byte[3] & 0xf0) == 0xe0)
	{
		...
	}
```

This bottom condition uses a bit operator to clear the lower four bits to make the first four bits `1110` (14, aka `e`). Nifty! And simpler than what I was going to write:

```C
if (byte[0] == 0xff &&
	byte[1] == 0xd8 &&
	byte[2] == 0xff &&
	byte[3] >= 0xe0 || byte[3] <= 0xef)
	{
		...
	}
```

### Other Stuff

One thing that really bothers me about writing code is that after I finish a program, it looks ***so simple***!!! When really it took hours upon hours to get it to be simple, and to get it to work. I guess it's a good thing but it's also like, ***this is so simple, how did I not figure this out sooner!?!!*** I'm even fooling myself, hah!

### Up Next

Turns out there is homework in the next CS50 session.