---
layout:     post
title:      Cryptography & Machine Learning With Python
author:     Nia
tags: 		  Python Cryptography
subtitle:  	Daily Review
category:   daily
---

Tonight there was a Machine Learning/Python meetup I went to. It was a talk about using the Metropolis-Hastings algorithm to decode text that's been scrambled beyond recognition. A lot of the mathematics were beyond what I've learned so far (I [*just* figured out](https://niamurrell.github.io/daily/2017/08/13/caesar-cipher/) how to write a Caesar cipher for goodness sakes!) but it was cool to see what can be done with the very-advanced version of these concepts. Let's see if I can explain what was happening...

First we used the novel War & Peace (in English) to train the program with the patterns & the probability of letters appearing next to each other in the English language. It made all of the text uniform and also looked at when non-letters appear in text (i.e. spaces, periods, etc.). With over 3.1 million characters to analyze, it's some robust source material. It took about 7 minutes to go through this process for War & Peace, and in the end generated  transition probability matrix (26x26 grid showing how likely each (non-)letter is to follow another (non-)letter) which can be used to decode any scrambled text. 

To decode text, a random mapping for each letter is set (so `g` maps to `a`, `o > b`, `v > c`, and so on, for example),and the Metropolis algorithm is used to apply this mapping to the encoded text, and then determine the log-likelihood that the mapping should be accepted, based on the probability matrix created from War & Peace. This algorithm is run repeatedly, changing the random letter mapping each time, and checking against the probability matrix to see if the current attempt makes sense in the English language. With each pass, it determines with increasing certainty what the correct mapping should be. We were able to feed it completely random scrambled passages of text, and it figured it out within a few minutes each time. It was pretty cool to see! For future reference here is the [repo](https://github.com/snooravi/meetups/tree/master/decryptation_example) for the tutorial we did.

This was also my first real introduction to Python code--pretty cool to see it being used in such a cool way. I'm looking forward to that coming up more and learning more about it.


### Up Next

No more after-work distractions this week...should be able to get back into the CS50 assignments, and hopefully finish the current section before the week is up!