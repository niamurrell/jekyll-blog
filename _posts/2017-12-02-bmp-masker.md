---
layout:     post
title:      BMP Masker
author:     Nia
tags: 		  C
subtitle:  	Daily Review
category:   daily
---

### C & BMP Masker

Today I worked on [a small program](https://github.com/niamurrell/bmpMask) in C to play with .bmp image files. I wrote a version of this for [CS50](https://niamurrell.github.io/search/index.html#CS50) to reveal a secret message as part of a homework assignment. Today I added a way to create secret messages of my own—fun stuff!

First I had to get C compiling and working locally on my computer since we use Cloud9 in CS50. Turns out it was already installed as part of the Xcode developer tools—I just needed to turn it on in the command line. [This link](https://stackoverflow.com/a/44246507/7432631) helped me figure that part out.

The message revealer program (`unmask.c`) reads a bitmap pixel by pixel and removes "noise" (red pixels) from the image, leaving a message that can be read by the naked eye. To write `mask.c` I swapped the colors so that it would add noise instead of removing it. It took a few tries to get the right kind of noise:

First I tried adding red every *n*th pixel; this only created stripes and didn't obscure the secret message at all. That was a bit of a ***duh*** hindsight moment--I'd ignored the fact that it's first looking row by row, not just pixel by pixel, so of course each row would have the same pattern of red pixels, thus creating stripes!

So then I learned how to generate random numbers in C: `int r = rand() % 10 + 1`. The `rand()` function creates a random number (integer in this case) between 0 and the modulo divisor, and I added 1 to avoid dividing by 0 which was causing errors in writing the output .bmp. 

With the randomness in place, I wrote my first pass only affecting the white pixels, to make sure that the hidden message would stay in tact. But this just made the message stand out more, completely defeating the purpose! So then I tried adding some white noise to the original image, thinking that it would help obscure things a bit better. Nope! After trying all sorts of things in Photoshop and the installing Gimp to try its brushes and failing, it was looking like there was no good way to modify the original image and make this work. And you shouldn't have to!—isn't that the whole point of creating the noise programmatically?

Well I took a long drive home from the coffee shop where I was ~~being frustrated~~ working and it dawned on me to just leave the message alone and run it through `mask` clean. And it worked! So now I can create hidden messages and unmask them too. Fun times.


### Other Stuff

I have been learning how to delete items from an array inside a database model based on user selection for the [value app](https://niamurrell.github.io/search/index.html#ValueApp). Everything I try isn't working but I'm almost there—now the only thing causing issue is the fact that the selected items are dates—I think because dates are mutable and the format of the date is different depending on how and when it's being displayed or selected. So still working on this...it's the last step before being able to finally deploy.


### Up Next

Travel is now complete for the year so no more breaks! I need to decide what I'm going to focus on for the next few weeks.