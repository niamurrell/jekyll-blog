---
layout:     post
title:      
author:     Nia
tags: 		  
subtitle:  	Daily Review
category:   daily
---

Database is up and running!!!!  ![PARTY!!!](http://emojis.slackmojis.com/emojis/images/1471045841/799/dancing.gif?1471045841) Wow that took some doing.

### MongoDB Install

I installed MongoDB and extracted the files at least 2 weeks ago but couldn't get it running. I tried so many tutorials and instructional videos but couldn't get passed the errors it was throwing...errors which of course weren't in the tutorials or videos!

In the end I got it to work by moving the folder containing the `/bin` directory (with all the binaries in it) to my root directory, although I still don't know if that was necessary. [This tutorial](https://treehouse.github.io/installation-guides/mac/mongo-mac.html) was a big help in the end, with a few parts I still had to figure out:
* One of its first instructions is to create the directory where the data files will live: `mkdir -p /data/db`. Apparently I don't have permissions to do this on my laptop and the request was denied. A comic I saw once came to mind, which got it to work!:

![sudo !!](https://i.kinja-img.com/gawker-media/image/upload/s--6Zf3kOc3--/c_fit,fl_progressive,q_80,w_636/780794572796342338.png)

* I also ran this command to make sure I have read/write access to the newly created directory: ```sudo chown -R `id -un` /data/db```

* Then I tried to run `mongod` to start the Mongo demon but the command was not found. I tried to check `mongo --version` to see if that was working (it had been working before, but with errors), and again the command was not found. Argh!

* So back to the [MongoDB docs](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/) where they say to ensure the MongoDB binaries folder is in your PATH by modifying the `.bashrc` file (and luckily I know what that is from [a few days ago](/2017-07-06-terminal-shortcuts.md)): `export PATH=path/to/mongodb/bin:$PATH`.

* Rather than restarting all my Terminal windows, I ran this command in my open Terminal window (and saved it to `.bashrc` for the next time). Then I ran `mongod` and lo and behold a server started running!

* Next opened a new Terminal tab to un `mongo` and got the lovely message:
```
Welcome to the MongoDB shell.
```

**Hooray!!**

A couple things to remember for future:

* To quit Mongo shell run `quit()`
* To stop the mongod server it's `ctrl + c`


### Other Stuff

Watched [a](https://www.youtube.com/watch?v=YhV4TaZaB84) [few](https://www.youtube.com/watch?v=sxToW3ixrwo) [videos](https://www.youtube.com/watch?v=5ySLQ5_cQ34) about pair programming and learned that it's a bit different to what I had imagined: two people working on the same code on one computer, with one person "driving" (writing the code) and the other "navigating" (figuring out what's next or what's needed), and switching off periodically. We tried this yesterday in a way in our group, but I guess it's a hard thing to do when no one knows even where to start! Will be interesting to give this a go on something I'm more comfortable with in the future.

### Up Next

Now that I got MongoDB running I can get going again on my bootcamp. Next steps are creating a simple database and then we learn about RESTful routing.

Still yet to get Postgres working on my machine for the group project so need to tackle that as well.
