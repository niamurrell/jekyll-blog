---
layout:     post
title:      Python Intro Continued
author:     Nia
tags: 		  Python
subtitle:  	Daily Review
category:   daily
---

Still working on this [CS50](https://niamurrell.github.io/search/#CS50) assignment. I've finished porting to Python some of the first programs we wrote in C. There are some really cool things Python does out of the gate that made me a little bit jealous! For example:

#### Iterating Through A String

We did a couple of [cipher programs](https://niamurrell.github.io//daily/2017/08/13/caesar-cipher/) to change a message from the user into a coded message. To write this in C it requires a **for loop** to manually go letter by letter:
```C
// prompt user for word to encode
printf("plaintext: ");
string plain = get_string();

// for each letter, shift by key and output cipher value
printf("ciphertext: ");
for (int i = 0, n = strlen(plain); i < n; i++)
{
	// do the shifting
}
```

The way that loops are written in Python makes it so much simpler! And being able to do this for a ***string***, not just an array or object, is pretty cool if you ask me:

```python
# prompt user for word to encode
print("plaintext: ", end="")
plain = cs50.get_string()

# for each letter, shift by key and output cipher value
print("ciphertext: ", end="")
for c in plain:
	# do the shifting
```

#### But...ASCII Values

One thing that I like in C that doesn't work in Python is the fact that characters (letters, numbers, etc.) are equivalent to their ASCII value, so `a == 97`, `A == 65`, etc. This made it pretty straightforward in the cipher exercises because you can just do simple addition or subtraction to shift the letters. In Python you have to explicitly change characters into numbers with `ord(char)`, do the manipulation, and then change it back to a letter with `chr(num)`. I think it's because Python forces type without needing the programmer to explicitly define type...so with characters they must be stored as strings? Anyway not the end of the world but I thought this was interesting.

### Up Next: Sentiment Analyzer

Next up we are writing a program to analyze the sentiment of someone's tweets using the [Natural Language Toolkit](http://www.nltk.org/) and the [Twitter API](https://developer.twitter.com/). Pretty big jump from our little cipher programs but I'm on it!
